# APTS computing1

标签（空格分隔）： 未分类

---

在此输入正文
Want: Compute the directional derivative ($\triangledown f(\theta)^T\delta,||\delta||=1$)
Truncation error:
$\|\frac{f(\theta+h\delta)-f(\theta)}{h}-(\triangledown f(\theta))^T\delta\|\leqslant \frac{hL_2}{2},\ \delta^T (\triangledown^2f(\centerdot))\delta\leqslant L_2$



taking comp $\{ \theta +b\delta\}$ into account, the sinple difference error, one side difference, that is minimized the by something is not nolonger for $\epsilon$ but some $h=\sqrt{ \epsilon}\sqrt{\frac{\delta l_0+2l_1||\theta||}{L_2}+\epsilon_0||\theta||^2}$. this outer one might, anyway, so this theory gives a theory for us to write a sofrware that maybe be trouble with, maybe. Don't have your model that far away from origin Nearly paralerrel, from origin. If you define your model in a well .
This things is go with the numerical deviratives.
The next is about opmization.


$\epsilon_0$=Machine $ double.eps

So using this when you know that you are double means. Other language of course there are other way to demonstrate this. C++ the opinion about this. So it is available.

Why we want to do this?

We are try to solve the computing ML difficult problem.
It become easily solve for the derivatives of things.
Might at some point have to compute this numerical.

find out evaluate compile it and run rest of your code.
That will be useful. Stan hamoltonian MCMC other package in R that TmB template model builder.

There are some bits in notes about this.

OPtimisation. 
Ex: we have the f here, use f as the density something, here is annoying we need both density and function as f.

Ex: $f(\theta)=-log\ p(y:\theta)$ or $-log p(y|\theta)-log p(\theta)$

loglikelihood based on parameter $\theta$.

What is the first thing you should do you start doing the optimization.
Look at the function, if possible draw a figure. That will less risk of problems.
The graph. THat's what we find look like. There something will

$f(\theta)$:$\mathbb{R}^n->\mathbb{R}$
another figure
$\theta$ for some other value, or make in between it might look like something more weird in the notes.

The challenge is to find the global minimize of the function, it hard either evaluate of the function everywhere, or there is structure in the function. For example, if the function structure is that it only have one minimal point then the local minimal is the gloval minimal.If you don't know how many local minimal are, it will be difficult to find the global one.

So, to find a local minimum if it exist.

Local thing to look into much, you can compute the optimum by hand, then of course you might able to show that minimal is.
However, the expression might be difficult that can't derict use the minimum.

you might just coding the log lk it self but not the other things like derivatives.

#Common principle

the first derivative is zero, the second derivative is positive,then it is the local minimum.

Sufficient criteria: $\triangledown f(\theta^*)=0,\triangledown^2 f(\theta^*)$ is pos def.

two cases, the function may not have derivatives at the minimum point.

1) start at some $\theta^{(0)}$
2) Find a descent that guarantee we are get closer, or at least reduce the function at that direction call it d; that basicallly says that $(\triangledown f(\theta^{(k)}))d<0$
3)Then we decide how far we go in that deriction.
 Find an $\alpha>0$ such that $f(\theta^{(k)}+\alpha d)<f(\theta ^{(k)})$; but this is not sufficient gurantee the convergence, then we take
$f(\theta^{(k)}+\alpha d)<f(\theta ^{(k)})+(\triangledown f(\theta^{(k)}))d\centerdot \epsilon \alpha/(\|d\|)>0 $,$\epsilon>0\approxeq10^{-16}$

Line search until $f(\theta)^{(k)}+\alpha d< ------|--|----$.

divide $\alpha$ by 2, a small step, to make sure the end up with small value forward.

There more clever way to do this, that's one more.
* do a polynomial approx using $f(\theta^{(k)},f(\theta^{(k)})+\alpha d),\triangledown f(\theta^{(k)}). =>\alpha$.
* End the point that exactly true. Cubic approximation. Try to take shorter steps and try again if failed.
4) let $\theta^{(k+1)}=\theta^{(k)}+\alpha d$

If you are in two dimension, think about it simplex method.
start witha  griangle, evaluate the function of these three points.
Here if $f_0>f_1 and f_2$
Go to the half point.
If that is far, if you small triangle and give the triangle bigger, finally to make the triangle small, shrinkage or somethings.

To meets that much detail to see ofc.
Also can look at the code for that.
Uses only f(.) doesn't need the derivatives.
that kind of function is fine. THe drawback is only use the 

This is robust but slower and safe to use if your function is little bit horrible.

How we find in such search.
gradient descent: $d=(-\triangledown f(\theta^{(k)}))/||\triangledown f(\theta^{(k)})||$ NOrmalising can make the steps less worry, in practice maybe to useconstant. try double if too small, if that works then use it. most accept eventually steps. If not accept then shrink it.
$d=(-\triangledown f(\theta^{(k)}))/||\triangledown f(\theta^{(k)})||+adaptive\ \ \ \ \ \alpha$
Newton:$d=-(\triangledown^2f(\theta^{(k)}))^{-1}(\triangledown f(\theta^{(k)}))$(from Taylor approx)
Remember the error we calculate before, that imply Newton is useful.
Problem: Unless you have good Hessian to calculate(program), gradient might easiler, computer the gradient is n, but the Hessian the N^q
[Note:$d=-B (\triangledown f(\theta^{(k)}))$ is a descent direction for any post def B.

Don't need the Hessian, we can use something else!

That is BFGS methods. That method, can update B^{(k)} -> B^{(k+1)} using only$ f(\theta^{(k)}),f(\theta^{(k+1)}),\triangledown f(\theta^{(k)}),\triangledown f(\theta^{(k+1)})
 $
so that $
B(\centerdot) \approxeq (\triangledown^2 f(\theta^{(k)}))
$

We then use the information we know about the function
Know that $-\triangledown_\theta^2 log[likelihoodfunction p(y;\theta)]$ is pof def at the mode of p(u;\theta).
 
Also know that $E_{y;\theta}(-\triangledown_\theta^2 log[ p(y;\theta)])$ For given model, and given theta, we takeexpectation over the data that

is pos def for all theta =expected fisher information.
The high order information are just disappear.
If you had the general models gaussian prior or things, the gaussian from is easy, it also easy for the data likelihood.
You do anything that works. We can do clever things if we know the likelihood function.
