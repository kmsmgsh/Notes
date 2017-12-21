# ATPS computing final

标签（空格分隔）： ATPS computing numerical notes

---

You will often what's statistics about.
statistics is not just about finding the best estimate or somehthing of the systemetic of uncertaintym but he is uncertainty
estimate of something instead : how uncertainty of something: relative to something.
Square error: also check wheter the prediction is

###Proper Scoring Rules

####Usual scenario: 
Here are two or more statistical methods, they might be frequencist or Bayes, producing other forecast or just prediction can be to the past as well. 
So for an unseen data points y,the prediction CDF,is F and  F',(for other method),
$S(F,y)$ be a score (or scoring rule)(or loss fun): give us answer that meaningful.

So imagine that actual distribution that y comes from is somethingthen we'd like the distribution match that.
So we can write another scenario for that:
####Scenario two: extension to the scenario 1:
We have training data $\mathit{Z}$,used for estimation
validation/test data Y used for checking.
Define, the average score is $\overline S(\{F_n\},\
\{y_k\} )=\frac{1}{m}\sum_{k=1} ^m S(F_k,y_k) $ if our method (F), conditional distribution for y given that,
It actually compute the true predictive distributions,so $\mathit{F}:\{y_n|\mathit{Z}\}\sim F_k$.
Then the score for is then 
$E(\overline S(\{F_n\},\
\{y_k\} )|\{ y_k\sim G_k  \})=E(\overline S(\{G_k\}|{y_k})|\{y_k\sim G_k\})$.

For two competition methods,
$\overline S(F,Y)<<\overline S(F,Y')$ indicates that F closer to G,(????? it S is a proper score.)
Expected score: $S(F,G)=E(S(F,y)|y\sim G)$
Proper score: $S(F,G)\geqslant S(G,G) $ for any F and G,
Strically proper score:
proper and $S(F,G)=S(G,G)$ iff $F=G$

Then just matter checking our loss function is proper or strically proper, if not proper: you can cheat, make 
keep the forecast truth.

$SE: S(F,y)=(y-m_F)^2,m_f=E(x|x\sim F)\\
S(F,G)=E((y-m_F)^2|y\sim G)=E((y-m_G+m_g-m_F)^2|y\sim G)\\
=E((y-m_G)^2|y\sim G)+(m_G-m_F)^2=\sigma_G^2+(m_G-m_F)^2
$
minimised for
$m_F=m_G$.$S_{se}$ is proper.
It is not strictly proper:

PMCC: predict model choice criterion.
Shich is  $S_{PMCC}=(y-m_F)^2+\sigma_F^2$
put penality on variance,if you look at the 
$S_{PMCC}(F,G)=\sigma_G^2+(m_G-m_F)^2+\sigma_F^2$
minimized for 
$m_F=m_G$
$\sigma_F^2=0$
Highly improper.
So don't use that.

Wuasi-Ignorance (QIQN)
$S(F,y)=\frac{(y-m_F)^2}{\sigma_F^2}+log(\sigma_F^2)$
$\sigma_F^2$ isnomarlised procedure.

$S(F,G)$ minimized for $m_F=m_G,\sigma^2 _F=\sigma^2_G$,it is proper.

So the likelihood as score:
Log-Score:
$S(F,y)=-log(p_F(y))$
$p_F$ is density or probability function for F
Then use Jensen's inequality shows $S_{LOG}(F,y)$ is strictly proper. that's the good and it is loglikelihood.
We might not compute this easily.

However, there more way to do this.
Absolute error,another score.
$S(F,y)=|y-F^{-1}(1/2)|$ is proper, w.r.t. the median of G.
put something else there, like mean.
generalising of this, look all quatiles, the cases might tricky.
Continues ranked probability score. (CRPS)
That is, $S_{CRPS}(F,y)=\int_R (F(x)-1(y\leqslant x))^2dx$,square first then different.
strictly proper:
$S(F,y)=\int (F(x)-G(x))^2dx+\int G(x)(1-G(x))dx$

Interval Score, which is minimized for $(F^{-1/2}(\alpha/2),F^{-1/2}(1-\alpha/2))=(G^{-1/2}(\alpha/2),G^{-1/2}(\alpha/2))$

log-score is also called IGN
that's why for Quasi-Ignorance

Gineitiny & Rafcony (2007) JASA, They use quick more complicated theory about these.

