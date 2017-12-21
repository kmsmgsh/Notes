# APTS computing 2

标签（空格分隔）： 未分类

---

在此输入正文
Newton opt.
Search dir $d=-(\triangledown ^2 f(\theta^{(k)}))^{-1}\triangledown f(\theta^{(k)})$
If that's isnot the positive definite, then you go the wrong way.
In small dimensions, replacing the matrix something else, one option is to take * $UAU^T=\triangledown ^2 f((\theta)^{(k)})$,replace with $Udiag(|\lambda_i|)U^T$ or $U diag(\lambda_i+\delta)U^T$.
Fisher scoring.
There are also some other option
Replace with $\triangledown ^2f+\delta I$ ,basically the same thing but the eigen values.
Check $\delta$ is large enough so that 
$d^T \{ \triangledown f(\theta^{(k)}) \}<0$
Trust region method,
=>THat's some option use to get  Quasi-Newton methods.


The next mini topic today is generating pseudo random numbers.

The most important lesson is following:

####Don't try this at home! (Unless you're into number theory)

Simple: Start at $X^{(0)}$
        Iterate $X^{k+1}=\{ ax^{k} +b\} mod M$, a,b,M integers
        if it looks random, it is random in most circumstance.
        Ex: a=65539,b=0,$M=2^{31}$
        Uniform quantile: is a nice straight line, perfect!
        we want generate the independent (fundmental dependency) hiding in the details of the integers.
        plot $x^k$ with $x^{k+1}$
        Clear dependence with the values.
        "Random"-> really bad!
        a better version:
        $a=69069$
        $b=1$
        $N=2^{32}$
        "Ripley's best!"
A proper 3D version, don't really see any structure in the figure. But ofc you can do better than this.

Much better to use hidden states.

You only see one of them.
You have no way to predict the value.
Mersene Twister.
Really unpredictable take wherever to start over beginning.

volume 3(2) of the D.knuth art of computer programming.

###Numerical integration
$I_\Omega=\int _\Omega f(x)dx,Ex: \Omega \subseteq \mathbb{R}^N,Ex: \Omega \subseteq \mathbb{S}^2->geo$,
$\mathbb{S}^2 \times \mathbb{R}$
Ex: Have $p_{x,y}(x,y)$ want $p_y(y)=\int p_{x,y}(x,y)dx$
Ex: Have $p_x(x)$, want $E(\phi(x)|x\sim p_x(\cdot))=\int \phi(x)p_x(x)dx$
Step 1 Look in Abramoriz &Stegun
            and Gradshteyn & Rhyzhik. There big books.
            A dictionary where you have triggle integral over function.
            A combination for them all.
            a integral for something like $\frac{cos(x)}{a+bx^2}$, some special cases maybe there are parameters $\frac{cos(cx)}{a+bx^2}$
            And online integrators. 
            
        Usually work a while,However, these all only cover 1-d integrals.
        
So, this oven doesn't help for that, you have to do something else.
That is determinist Quadrature rules,
for $\int ^b _a f(x)dx,\Omega=[a,b]$
0).Midpoint rule, that one yet says that $\hat I_\Omega=\frac{b-a}{N} \sum ^N _{k=1} f(a+(k-\frac{1}{2})\cdot \frac{b-a}{N})$ Called inside f is $x_k$ function in the middle of disjoint split interval from [a,b].
1)Troperzerdel rule0
Piecewise linear function



2) Simpson's rules

3) Gaussian Quadratic: If g(x) is any pollynomial of degree 2N-1 and w(x) is known and "special", it's known function, then $\int _a ^b w(x)f(x)dx$ product polynomial for the special function, is excatly equals to $\sum ^N _{k=1}w_kg(x_k)$ for a specific set $\{(x_1,w_1),...(x_N,w_N)\}$.
So one such case, Gauss-Hermite $\Omega \in R,w(x)=e^{-x^2}$,we have Gauss-Legendre: $\Omega =[a,b],w(x)\equiv 1$

In small intervals, it is always really polynomials by Taylor,
In general
$\int ^b _a f(x)dx=\int _a ^b w(x)\frac{f(x)}{w(x)}dx \simeq \sum _{k=1}^N w_k \frac{f(x_k)}{w(x_k)}$ Note: $w_k \neq w(x_k)$

GQ converge much faster than Simpson's rule.
Constructing the points.

We have two methods to talk about

Laplace approximation (4.4.3)
Forgot about the cases very high dimensions, you can hardly compute things unless in a small intervals.

So, Ex: $b\sim N(0,\Sigma_b(\theta)),y_i|b_i\sim Po(e^{b_i})$, any time model, Find $p_y(y|\theta)=\int p_{y,b} (y,b|\theta)db=p_{y|b,\theta}(y)p_{b|\theta}(b)db$, we know b is gaussian, we could try something like Gaussian density

midpoint rule: bias $\sim O(N^{-\frac{2}{n}})$ not increase dramatically in dimension N.

So what can we do? We can use optimization
$p_y(y|\theta)\simeq p_{y,b}(y,\hat b_{y,b})\cdot \int exp(-\frac{1}{2}(b-\hat b_{b,\theta})^T\hat H_{y,\theta}(y-\hat b_{y,\theta}))db$
$(\hat b_{y,\theta}=arg min_b)\{-log p_{y,b}(y,b)\},\hat H_{y,b}=-\triangledown ^2 log p_{y,b}(y,\hat b_{y,\theta})$

$p_{y|theta}(y|theta)\simeq p_{y,b} (y,\hat b_{y\theta}\cdot \frac{(2n)^{n/2}}{\{det \hat H _{y,\theta}\}^{1/2}})$
=> INLA r-inla.org

Monte Carlo
Std.dev. based on independent samples $\sim O(N^{-1/2})$
Loses if n<4, wins if n>4

$I_\Omega=E(f(x)|x\sim\frac{1}{|\Omega|on \Omega})\cdot |\Omega|\simeq \frac{|\Omega|}{N} \sum ^N _{k=1} f(x_{k}),x_k\sim Unif(\Omega)$

Variance Reduction Methods
Importance sampling E(f(x)|x\sim Unif(\Omega))=
$\int_\Omega f(x)dx=\int _\Omega g(x)\cdot \frac{f(x)}{g(x)dx}\simeq \frac{1}{N}\sum ^n_{k=1}\frac{f(x_k)}{g(x_k)},x_k \sim g(\cdot)$.
So if we can find g is similar to f this value is more similar to f and 
