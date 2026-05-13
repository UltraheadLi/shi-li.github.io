* Learning materials: Richard L. Smith, S. Clémençon1 & A. Sabourin, Stuart Coles

# 1 Introduction

## 1. Introduction to GEV

Let's use an example to introduce the problem we are studying. We know that car tires continuously wear out over years of use, and there are two main reasons for them being scrapped: 

* The cumulative degree of wear exceeds a certain scrapping threshold, making the tire unable to be used further. 


* A sudden event (such as an accidental collision or falling into a pothole, etc.) causes massive one-time damage exceeding a certain scrapping threshold. 



For these two scrapping pathways, we respectively care about the partial sums and partial maxima of the degree of damage over long-term use. If we can characterize the distributions of partial sums and partial maxima, we can characterize the probability of a tire being scrapped within a certain period of use.

The well-known CLT is the theory that characterizes the asymptotic properties of the partial sum $S_{n}$ of a sequence of random variables. The Lindeberg-Levy theorem tells us that for i.i.d. random variables $X_{1}, X_{2}, ..., X_{n}, ...$ with expected value and variance $E(X_{1})=\mu$ and $Var(X_{1})=\sigma^{2}>0$, there is a standard normal limit distribution for the partial sum $S_{n}=\sum_{i=1}^{n}X_{i}$: 

$$\frac{S_{n}-n\mu}{\sigma\sqrt{n}}\rightarrow N(0,1) , n\rightarrow\infty,$$



That is: 

$$lim_{n\rightarrow\infty}Pr\left(\frac{S_{n}-n\mu}{\sigma\sqrt{n}}\le x\right)=\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{x}e^{-\frac{t^{2}}{2}}dt=\Phi(x),$$



where $\Phi(x)$ is the distribution function of the standard normal distribution.

The asymptotic theory of sample extremes developed practically in parallel with the CLT, and there are certain similarities between the two. We assume $F$ is the distribution function of the random variable $X$, and define $x^{*}:=sup\{x:F(x)<1\}$ as the right endpoint of the support set (note that $x^{*}$ can be infinity). Then the sample partial maxima converge in probability to the right endpoint, i.e., 

$$max(X_{1},X_{2},...,X_{n})\rightarrow x^{*}, n\rightarrow\infty.$$



It is a intuitive equation. More strictly: 

$$\forall\delta>0, Pr(|max(X_{1},...,X_{n})-x^{*}|>\delta)=Pr(max(X_{1},...,X_{n})<x^{*}-\delta)=(F(x^{*}-\delta))^{n}\rightarrow0,$$



where since $x^{*}:=sup\{x:F(x)<1\}$, we have $0\le F(x^{*}-\delta)<1$.

Above we established the consistency of sample partial maxima, now we care about its asymptotic properties, namely **whether $max(X_{1},...,X_{n})$ has a non-degenerate limit distribution**, just like the partial sum $S_{n}$. To obtain a more standardized limit distribution, the idea of standardization is essential.

Now we assume there exist constant sequences $a_{n}>0$, and $b_{n}\in\mathbb{R}$ $(n=1,2,...)$, such that the standardized sample partial maxima $\frac{max(X_{1},X_{2},...,X_{n})-b_{n}}{a_{n}}$ have a non-degenerate limit distribution $G(x)$, i.e., 

$$lim_{n\rightarrow\infty}F^{n}(a_{n}x+b_{n})=G(x), n\rightarrow\infty$$



holds for all continuity points of $G(x)$.

We now care about the properties and specific form of $G(x)$. Below, we first give several equivalent representations of the first-order limit condition for extremes, and then derive the generalized extreme value distribution $G_{\gamma}(x)$ based on these conditions.

---

## 2. Equivalent Representations of the First-Order Limit Condition for Extremes 

Let $F$ be the distribution function of $X$, $a_{n}>0$ and $b_{n}$ be two sequences of real constants, and $G$ be a non-degenerate distribution function. The following three statements are equivalent: 

**1**. For any continuity point of $G$, as $n\rightarrow\infty$, there exist $a_{n}>0$, $b_{n}$, such that: 

$$lim_{n\rightarrow\infty}F^{n}(a_{n}x+b_{n})=G(x);$$

**2**. For any continuity point of $G$ satisfying $0<G(x)<1$, let $a(t):=a_{[t]}$, and $b(t):=b_{[t]}$ ($[t]$ represents the integer part of $t$), we have:

$$lim_{t\rightarrow\infty}t(1-F(a(t)x+b(t)))=-log~G(x);$$

**3**. Define $U(t):=F^{\leftarrow}\left(1-\frac{1}{t}\right)$ as the tail quantile function of $X$. 

For instance, if $X$ represents the annual rainfall of a place, when $t=1000$, $U(t)$ represents the 1-in-1000-year rainfall, i.e., the 99.9% lower quantile of $X$. For any continuity point $x>0$ of the function $D(x)=G^{\leftarrow}(e^{-1/x})$, there exist $a(t):=a_{[t]}$ and $b(t):=b_{[t]}$, such that:



$$lim_{t\rightarrow\infty}\frac{U(tx)-b(t)}{a(t)}=D(x).$$






The three expressions above characterize the first-order conditions of the extreme value distribution from three perspectives: (1) Cumulative distribution function; (2) Survival function; (3) Quantile function. The proof for $(1)\iff(2)$ uses logarithmic operations; $(2)\iff(3)$ uses inverse function operations. A rough proof is as follows: 

**Proof of (1) $\Rightarrow$ (2):** First, taking the logarithm of both sides of the limit expression in (1) yields:


$$lim_{n\rightarrow\infty}n~log~F(a_{n}x+b_{n})=log~G(x).$$

Clearly, there exist $a_{n}>0, b_{n}$ such that $F(a_{n}x+b_{n})\rightarrow1$ (it is said that in applications, usually choose a larger $b_{n}$ as the threshold, satisfying $b_{n}\rightarrow x^{*}$). Then $(F(a_{n}x+b_{n})-1)$ is an equivalent infinitesimal quantity to $log~F(a_{n}x+b_{n})$, therefore we have:


$$lim_{n\rightarrow\infty}n(F(a_{n}x+b_{n})-1)=log~G(x).$$

Replacing the discrete subscript $n$ with a continuous subscript $t$, while $a(t):=a_{[t]}, b(t):=b_{[t]}$, we get:


$$lim_{t\rightarrow\infty}t(1-F(a(t)x+b(t)))=-log~G(x).$$



**Proof of (2) $\Rightarrow$ (3):** From (2), we can get: 

$$lim_{n\rightarrow\infty}n(1-F(a_{n}x+b_{n}))=-log~G(x).$$

Viewing the left expression as a function of $x$, $H_{n}(x)=n(1-F(a_{n}x+b_{n}))$, its limit function is $H(x)=-log~G(x)$. According to the limit properties of inverse functions (if a function sequence converges pointwise to a strictly monotonic function, then its inverse function sequence also converges to the inverse of that limit function), we have $H_{n}^{\leftarrow}(z)\rightarrow H^{\leftarrow}(z)$. Calculating $H_{n}^{\leftarrow}(z)$: solving $z=n(1-F(a_{n}x+b_{n}))$ gives $F(a_{n}x+b_{n})=1-z/n$, hence $a_{n}x+b_{n}=F^{\leftarrow}(1-z/n)$, therefore:


$$H_{n}^{\leftarrow}(z)=\frac{F^{\leftarrow}(1-z/n)-b_{n}}{a_{n}}.$$

And $H^{\leftarrow}(z)=G^{\leftarrow}(e^{-z})$. Specifically, taking $z=1/x$ $(x>0)$, we get:


$$\frac{U(nx)-b_{n}}{a_{n}}=\frac{F^{\leftarrow}(1-1/(nx))-b_{n}}{a_{n}}\rightarrow G^{\leftarrow}(e^{-1/x})=:D(x),$$

Rewriting with continuous subscript $t$ yields expression (3).

*Note regarding inverse functions:* 

$$\begin{cases}U(t)=F^{\leftarrow}\left(1-\frac{1}{t}\right)=\left(\frac{1}{1-F(t)}\right)^{\leftarrow}\\ D(x)=G^{\leftarrow}(e^{-1/x})=\left(-\frac{1}{log~G(x)}\right)^{\leftarrow}\end{cases}$$



---

## 3. Derivation of the Functional Form of the Generalized Extreme Value Distribution 

In this section, we derive the specific form of the limit distribution $G(x)$. From the quantile form of the first-order condition, we know that for any continuity point $x>0$: 

$$lim_{t\rightarrow\infty}\frac{U(tx)-U(t)}{a(t)}=D(x)-D(1)=:E(x)$$



Here we assumed that $1$ is a continuity point of $D(x)$. Next, we explore the properties of the function $E(x)$. For any given $y>0$: 

$$\frac{U(txy)-U(t)}{a(t)}=\frac{U(txy)-U(ty)}{a(ty)}\cdot\frac{a(ty)}{a(t)}+\frac{U(ty)-U(t)}{a(t)};$$



We assert that the limits $lim_{t\rightarrow\infty}\frac{a(ty)}{a(t)}=A(y)$ and $lim_{t\rightarrow\infty}\frac{U(ty)-U(t)}{a(t)}=E(y)$ exist , which gives:

$$lim_{t\rightarrow\infty}\frac{U(txy)-U(t)}{a(t)}=lim_{t\rightarrow\infty}\frac{U(txy)-U(ty)}{a(ty)}\cdot lim_{t\rightarrow\infty}\frac{a(ty)}{a(t)}+lim_{t\rightarrow\infty}\frac{U(ty)-U(t)}{a(t)}$$



i.e.,


$$E(xy)=E(x)A(y)+E(y), \forall x,y>0.$$



To align the condition with differential equation conditions, the property of $E(x)$ contains a product term $xy$. We want properties regarding sum terms, so let $s:=log~x, t:=log~y, H(x):=E(e^{x})$, then $x=e^{s}, y=e^{t}, H(s)=E(x), H(t) = E(y)$, and:

$$H(s+t)=E(xy)=H(s)A(e^{t})+H(t)$$



Knowing that $H(0)=E(1)=0$, we let $x,y\ne1$ so that $s,t\ne0$, resulting in: 

$$\frac{H(s+t)-H(t)}{s}=\frac{H(s)-H(0)}{s}A(e^{t})$$



Assuming $H(t)$ is differentiable everywhere , letting $s\rightarrow0$ and taking the limit of the above equation yields: 

$$H^{\prime}(t)=H^{\prime}(0)A(e^{t})$$



Finally, to eliminate the $A(\cdot)$ function, we assume $H^{\prime}(0)\ne0$ and let $Q(t):=H(t)/H^{\prime}(0)$. Then $Q(0)=0, Q^{\prime}(0)=1$, and: 

$$Q(s+t)=Q(s)A(e^{t})+Q(t)=Q(s)Q^{\prime}(t)+Q(t),$$



From the symmetry of $s$ and $t$, we further obtain: 

$$Q(s)Q^{\prime}(t)+Q(t)=Q(t)Q^{\prime}(s)+Q(s).$$



Rearranging yields: 

$$\frac{Q(s)-Q(0)}{s}[Q^{\prime}(t)-1]=\frac{Q(t)}{s}[Q^{\prime}(s)-Q^{\prime}(0)]$$



Letting $s\rightarrow0$ and taking the limit yields: 

$$Q(t)Q^{\prime\prime}(0)=Q^{\prime}(t)-1,$$



Which means: 

$$\frac{Q(t)-Q(0)}{t}Q^{\prime\prime}(0)=\frac{Q^{\prime}(t)-Q^{\prime}(0)}{t}$$



Letting $t\rightarrow0$ and taking the limit yields $Q^{\prime}(t)Q^{\prime\prime}(0)=Q^{\prime\prime}(t)$.

Knowing $Q(0)=0, Q^{\prime}(0)=1$, and assuming $Q^{\prime\prime}(0)=\gamma\in\mathbb{R}$, the problem transforms into solving a standard ordinary differential equation. It is easy to obtain: 

$$(log~Q^{\prime})^{\prime}(t)=Q^{\prime\prime}(0)=\gamma$$



$$log~Q^{\prime}(t)=\gamma t+log~Q^{\prime}(0)=\gamma t$$



$$Q^{\prime}(t)=e^{\gamma t}$$



$$Q(t)=\int_{0}^{t}e^{\gamma s}ds+Q(0)=\frac{e^{\gamma t}-1}{\gamma}$$



$$H(t)=H^{\prime}(0)\frac{e^{\gamma t}-1}{\gamma}$$



$$D(y)=D(1)+E(y)=D(1)+H(t)=D(1)+H^{\prime}(0)\frac{y^{\gamma}-1}{\gamma}$$



$$D^{\leftarrow}(y)=\left(1+\gamma\frac{y-D(1)}{H^{\prime}(0)}\right)^{1/\gamma}>0 \text{ (since } y>0)$$



Also $D^{\leftarrow}(y)=-1/log~G(y)$. Substituting, we get:

$$G(x)=exp\left(-\left(1+\gamma\frac{x-D(1)}{H^{\prime}(0)}\right)^{-1/\gamma}\right)$$



It is easy to know that $H(t)$ is monotonically non-decreasing, and assuming $H^{\prime}(0)\ne0$, then $H^{\prime}(0):=\sigma>0$ is the scale parameter and $D(1):=\mu$ is the location parameter. What is obtained is actually a three-parameter generalized extreme value distribution. Standardizing it (eliminating the effects of location and scale parameters) by setting $\mu=0$ and $\sigma=1$, we get the single-parameter generalized extreme value distribution form: 

$$G_{\gamma}(x)=exp(-(1+\gamma x)^{-1/\gamma}), 1+\gamma x>0$$



---

## 4. Three Subclasses of Generalized Extreme Value Distribution 

Observing that the image shapes for $\gamma>0$, $\gamma=0$, and $\gamma<0$ are noticeably different, the generalized extreme value distribution $G_{\gamma}$ can be divided into three subclasses based on this: 

### (a) 

Fréchet Distribution Family 

For $\gamma>0$, we have $\forall x: 1+\gamma x>0$, $G_{\gamma}(x)<1$, meaning the right support endpoint of $G_{\gamma}(x)$ is $x^{*}=+\infty$. Furthermore, as $x\rightarrow\infty$, we have the equivalent infinitesimal:


$$1-G_{\gamma}(x)=1-exp(-(1+\gamma x)^{-1/\gamma})\sim(1+\gamma x)^{-1/\gamma}\sim\gamma^{-1/\gamma}x^{-1/\gamma},$$

This means the survival function corresponding to $G_{\gamma}(x)$ decays as a power function in the right tail (polynomial function decay). Thus, it is right heavy-tailed, and the tail index is $1/\gamma$. Therefore, moments $E(X^k)$ of any order greater than $1/\gamma$ do not exist. If we let $\alpha=1/\gamma>0$, then $\Phi_{\alpha}(x)=G_{\gamma}((x-1)/\gamma)=exp(-x^{-\alpha})$ is called the Fréchet distribution family. Its domain is $x>0$, representing the class of generalized extreme value distributions where $\gamma>0$.

### (b) 

Gumbel Distribution 

For $\gamma=0$, we similarly have $\forall x\in\mathbb{R}$, $G_{0}(x)=exp(-e^{-x})<1$, meaning the right support endpoint is $+\infty$. However, since $1-G_{0}(x)\sim e^{-x}$ as $x\rightarrow\infty$, the survival function decays exponentially in the right tail. Therefore $G_{0}(x)$ is a light-tailed distribution, and moments of any order exist. We call $G_{0}(x)$ the double-exponential distribution or Gumbel distribution.

### (c) 

Reverse-Weibull Distribution Family 

For $\gamma<0$, according to the domain of $G_{\gamma}(x)$, we have $x<-1/\gamma$. Thus, $G_{\gamma}(x)$ has a finite right support endpoint, and its distribution is short-tailed. Observing that:


$$1-G_{\gamma}(-1/\gamma-x)\sim(-\gamma x)^{-1/\gamma}\rightarrow0, x>0,$$

it can be generally seen that when $x>0$, the survival function rapidly approaches 0, corroborating its short-tail characteristic. Letting $\alpha=-1/\gamma>0$, then $\Psi_{\alpha}(x)=G_{\gamma}(-(1+x)/\gamma)=exp(-(-x)^{\alpha})$ is called the reverse-Weibull distribution family, and its domain is $x\le0$.

***

# 2 Limit Theory for Univariate Extremes
