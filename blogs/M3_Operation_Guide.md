# M3 Supercomputer Operation Guide | M3 超算操作指南

This document outlines the standard workflow for running R parallel computing tasks on the M3 cluster.
本文档概述了在 M3 集群上运行 R 语言并行计算任务的标准工作流程。

---

## 1. Preparation Phase | 准备阶段

### 1.1 Network Connection | 网络连接
* **On Campus (校内):** Connect directly to **eduroam**. No VPN required.
    * **校内:** 直接连接 **eduroam**。无需开启 VPN。
* **Off Campus (校外):** Connect to **Monash GlobalProtect VPN** (vpn.monash.edu) first.
    * **校外:** 必须先连接 **Monash GlobalProtect VPN** (vpn.monash.edu)。

### 1.2 Environment Setup | 环境配置
Before submitting, ensure all R packages are installed in your personal library.
在提交之前，确保所有 R 包已安装在个人库中。
* **CRAN Packages:** `install.packages(c("doParallel", "foreach", "doRNG", "robustbase"))`
* **GitHub Packages:** `remotes::install_github("author/repo")`
* **Module Load:** Always load the R module in terminal: `module load R`.
    * **模块加载:** 在终端执行 `module load R` 以启用 R 环境。

### 1.3 Code Verification | 代码核对
* **Parallel Logic:** Use `furrr::future_map_dfr` with `furrr_options(seed = TRUE)` for thread-safe random seeds. Do **not** manually call `set.seed()` inside worker functions — it has no effect and gives a false sense of reproducibility.
    * **并行逻辑:** 使用 `furrr::future_map_dfr` 配合 `furrr_options(seed = TRUE)` 确保多线程随机数种子安全。**不要**在 worker 函数内手动调用 `set.seed()`，该调用在并行环境中无效。
* **CPU Detection:** Use the following block to auto-detect SLURM cores vs local cores. Place this in your script **before** `plan(multisession, ...)`.
    * **核数检测:** 使用以下代码块自动识别超算或本地环境，置于 `plan(multisession, ...)` 之前。

```r
library(future)
library(furrr)

slurm_cpus <- Sys.getenv("SLURM_CPUS_PER_TASK")
if (slurm_cpus != "") {
  num_workers <- as.numeric(slurm_cpus)
  cat(sprintf("Detected SLURM environment, using %d workers.\n", num_workers))
} else {
  num_workers <- max(1, parallel::detectCores() - 2)
  cat(sprintf("Local environment, using %d workers.\n", num_workers))
}
plan(multisession, workers = num_workers)
```

* **Expected Row Count:** Never hardcode `expected_rows`. Derive it from the grid to avoid silent diagnostic errors.
    * **预期行数:** 不要硬编码 `expected_rows`，应从参数网格动态计算，避免诊断结果静默出错。

```r
# ✅ Correct | 正确写法
expected_rows <- nrow(param_grid) * sim_params$n_iters

# ❌ Avoid | 避免写法
# expected_rows <- 57600
```

* **Pathing:** Ensure all `source()` paths and `saveRDS()` paths are correct relative to the project root.
    * **路径检查:** 确保所有 `source()` 和 `saveRDS()` 的路径相对于项目根目录是正确的。

---

## 2. Starting Phase | 开始阶段

### 2.1 Prepare the Submit Script | 准备提交脚本
Create/edit `scripts/submit.sh` with Slurm parameters:
创建或编辑 `scripts/submit.sh`，配置 Slurm 参数：
```bash
#SBATCH --cpus-per-task=32
#SBATCH --mem=64G
#SBATCH --time=02:00:00
```

### 2.2 Submit the Job | 提交任务
In the Positron Terminal (ensure you are in the project root):
在 Positron 终端中（确保处于项目根目录）：
```bash
sbatch scripts/submit.sh
```

---

## 3. Tracking Phase | 跟踪阶段

### 3.1 Monitor Queue | 监控队列
Check the status of your job (R = Running, PD = Pending):
查看任务状态（R 为运行中，PD 为排队中）：
```bash
squeue -u YOUR_USERNAME
```

### 3.2 Inspect Logs | 查看日志
Monitor the real-time output in the `output/` folder:
查看 `output/` 文件夹中的实时日志：
* Find the `.out` file named with your Job ID.
    * 找到以 Job ID 命名的 `.out` 文件。
* Use `tail -f output/your_log.out` to watch live updates.
    * 使用 `tail -f` 命令查看滚动更新。

---

## 4. Closing Phase | 结束阶段

### 4.1 Download Results | 下载结果
Once the job is finished (disappears from `squeue`):
任务运行结束（从 `squeue` 列表中消失）后：
* Locate the `.rds` or `.csv` files in your project folder.
    * 在项目文件夹中找到生成的 `.rds` 或 `.csv` 文件。
* Right-click the file in Positron Explorer and select **Download**.
    * 在 Positron 资源管理器中右键点击文件，选择 **Download** 下载到本地。

### 4.2 Clean Up | 清理
* Delete unnecessary large log files to save quota.
    * 删除不必要的大型日志文件以节省存储空间。
* Close the Positron Remote connection to release local resources.
    * 关闭 Positron 远程连接以释放本地资源。

---
**Author:** Shi Li  
**Target System:** M3 Massive (Monash University)
