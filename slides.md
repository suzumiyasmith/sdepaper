<!-- $theme: gaia -->

# Stochastic calculus and risk-neutral pricing: 
## theory and computation


Fengguang Wang
Student ID:$426920$

---
<!-- page_number: true -->

# Overview


- Stochastic process
- SDEs & their numerical solution
- An algeric way to risk-neutral pricing in discrete situation


---

# Stochastic process

Preliminaries 

---

# Filtration
A probability space $(\Omega, \mathcal{F}, P)$
equipped with filtration $(\mathcal{F}_i)_{i \in I}$ of $\sigma$-algebra $\mathcal{F}$,
is a filtered probability space.

---

# Adapted
> past & now

For a stochastic process $X: I \times \Omega \rightarrow S$ under
a filtered probability space with filtration $(\mathcal{F}_i)_{i \in I}$,
X is called an adapted process if $\forall i \in I, X_i: \Omega \rightarrow S$ is a $(\mathcal{F}_i, \Sigma)$-measurable function

---

# Predicatable

> past

For a stochastic process $X: I \times \Omega \rightarrow S$ under
a filtered probability space with filtration $(\mathcal{F}_i)_{i \in I}$,
X is called a predictable process if 
$\forall i \in I, j = {max}_{k\in I,k<i}k, X_i: \Omega \rightarrow S$ is a $(\mathcal{F}_j, \Sigma)$-measurable function

---

# Markov

> now

In a filtered probability space $(\Omega, \mathcal{F}, (\mathcal{F}_i)_{i \in I}, P)$,
An adapted process $X : I \times \Omega \rightarrow S$ s.t.
$$\forall s < t \in I, P(X_t \in A | \mathcal{F}_s) = P(X_t \in A | X_s) $$
is called Markov process.

---

# Stochastic Differential Equation 

---

# Ito integral


In Ito calculus, integral of stochastic process is defined as      
$$ \int_0^t H dW = \lim_{n \rightarrow +\infty} \sum_{[t_{i-1},t_i]\in \pi_n} H_{t_{i-1}}(W_{t_i} - W_{t_{i-1}}) $$
      
where $W$ is a semimartingale,
and H is a cadlag adapted process of locally bounded variation


---

# SDE

For integral equation of the form
      
$$ X_{t+s} - X_t = \sum_{i<n} \int_t^{t+s} H_i dW_i$$
its differential form
$$ dX = \sum_{i<n} H_i dW_i$$
is called SDE.

---

# Numerical Simulation

---

# Discretisation

Basic idea of simulating numerical solution of a SDE is discretisation.

For SDE $dX_t=a(t, X_t)dt + b(t, X_t)dW_t$,
  chop the interval $[0,T]$ into $N$ grid which has $\Delta t = \frac{T}{N}$ interval.
  

And via discretisation, continuous stochastic process becomes a discrete-time Markov chain in a given scheme D.

$Y_{n+1} = Y_n + D(Y_n,\Delta t,\Delta W)$

---

# Schemes

Euler-Maruyama approximation:

$$D = D_L = a(X_n)\Delta t + b(X_n)\Delta W_n$$

Milstein approximation:
        
$$D= D_L+$$
$$\frac{1}{2} b(X_n)b'(X_n)((\Delta W_n)^2 - \Delta t) $$

---

Runge-Kutta approximation:
        
$$D= D_L+$$
$$\frac{1}{2} (b(\hat{X}_n) - b(X_n))((\Delta W_n)^2 - \Delta t)(\Delta t)^{-1/2} $$
        
where
$$\hat{X}_n = X_n + a(X_n)\Delta t + b(X_n)\sqrt{\Delta t}$$


---

# Benchmarks

for SDEs in form of

$dX = \mu(X,t)dt + \sigma(X,t)dW$

take simulation using Euler-Maruyama scheme in a finer grid as the exact solution 

---

$\mu = 0.1 * X$
$\sigma = 0.8 * X$
$X_0 = 1$

![alt text](plot/trial_1.svg "")

---

$\mu = 0.1 * X$
$\sigma = 0.8 * sin(10 * t) * {X}$
$X_0 = 1$

![alt text](plot/trial_7.svg "")

---

$\mu = 0.1 * X$
$\sigma = 0.8 * sin(10 * t) * \sqrt{X}$
$X_0 = 1$

![alt text](plot/trial_13.svg "")

---

$\mu = 0.1 * X$
$\sigma = 0.8 * sin(10 * t) * sin(5*t *{X})$
$X_0 = 1$

![alt text](plot/trial_19.svg "")

---

# Discretisation

#### SDE $\rightarrow$ discrete-time Markov chain

Trade-off: Local linearity

anlysis $\rightarrow$ algebra

---

# Algebric Way to Risk Nutral Pricing in a discretised world

---

# Motivation

- Rube-Goldberg machine
- overkill
- formalisation

---

# Intuition

- commodities: 
  - Algebra over a Field
- composable and programable transaction:
  - Bicartesian Closed Category
- diverable future: 
  - Temporal Logic & Free Monad

---

## Preliminaries

Algebra over a field: 
  Let K be a field, and let A be a vector space over K equipped with an additional binary operation A × A $\rightarrow$ A 
  
  Then A is an algebra over K if :
    Right distributivity: (x + y) · z = x · z + y · z
    Left distributivity: x · (y + z) = x · y + x · z
    Compatibility with scalars: (ax) · (by) = (ab) (x · y) 

---

Bicartesian Closed Category:
  A category closed under product, coproduct and exponential s.t.
  
    (xy)z = (xz)y.
    x×(y×z) = (x×y)×z
    x×y = y×x
    x×1 = x (here 1 denotes the terminal object of C)
    1x = 1
    x1 = x
    (x×y)z = xz×yz
    (xy)z = x(y×z)
    x + y = y + x
    (x + y) + z = x + (y + z)
    x×(y + z) = x×y + x×z
    x(y + z) = xy×xz
    0 + x = x
    x×0 = 0
    x0 = 1

---

Temporal  logic as Functor and Free Monad:
  
  Functor:
  pure : a -> f(a)
  map: (a -> b) -> (f(a) -> f(b))
  s.t. functor rules
  
  Free: (f is a functor)
  pure : a -> Free(f)(a)
  impure : f (Free(f)(a)) -> Free(f)(a)
  
  Then Free f is a monad s.t. monad rules

---

# Formal Defination

Comodities:

Comodity category $C$ is group generated with $\otimes$ ,$\oplus$ by base comoditiy object $O_i(i\in I)$ over field $R$ 
Comodity is bicartesian closed with exponential $\rightarrow$, product $\otimes$ with terminal object 1
and coproduct $\oplus$ with initial object 0
Comodity is equiped with Functor: Next:
  next: (W -> C) -> Next C
  pure c = next (const(c))
  map f (next(g)) = next (f . g)

---
Then $M(a) = Free(Next(a))$ is a free monad
we denote category $M(C)$ as general comodity category $N$

$\otimes$ ,$\oplus$ and $\rightarrow$ also works on $N$

---

# Application

---
# discretise SDE as time-discrete Markov Chain

for SDE :$dX= \mu dt + \sigma dW$

discretised as

$Y_{n+1} = Y_n + D(Y_n,\Delta W)$

---

represented as
$y_0 = pure(y_0)$
$y_n=$
$$ next (w_1 \rightarrow $$
$$ next(w_2 \rightarrow$$
$$\cdots$$
$$ next(w_n \rightarrow$$
$$(\Sigma_i(D(y_i,w_i))+y_0)\cdots))$$

---

# Risk Neutral pricing
assuam $O_1$ is money and $O_2$ is a risky stock
European option expired in n steps later:

---
$p_k : Free(Next)(C) \rightarrow Free (Next)(C)$
$$ p_k = $$
$$ next (w_1 \rightarrow $$
$$ next(w_2 \rightarrow$$
$$\cdots$$
$$ next(w_n \rightarrow$$
$$(k \cdot O_1) \rightarrow (1 \cdot O_2))\cdots))$$

---

"Realise" Future by paired Functor
$Observe :$
$observe : (\Omega \rightarrow W) \rightarrow Observe(W)$

$pair : Free(Next)(C) \rightarrow Observe(W) \rightarrow C$
$pair =impure(f)(f_0) \mapsto impure(g)(g_0)$
$\mapsto (f_0 . g_0) + pair(f)( g) )$

---
# Question

---

# Thanks
