# Quiz 4


## Instructions

>  Write your name at the top right.  You are to work on this quiz alone without any help 
>  from any other resource <b>except for a single $8.5 \times 11$ inch page of handwritten notes</b>.  
>  This quiz will be ungraded but must be handed in for attendance. 


## Problems:

### Problem 1:

In this problem, we will only assume the following: 
$$n, p \geq 2 $$  
and let $\mathbf{X}\in \mathbb{R}^{n \times p}$.

Define $\mathbf{X}^\dagger = \left(\mathbf{X}^\mathrm{T} \mathbf{X}\right)^{-1} \mathbf{X}^\mathrm{T}$. Carefully compute the value of the product $\mathbf{X}^\dagger \mathbf{X}.$

<div class="solutions">
#### Solution:
We remark, while we assume that $\left(\mathbf{X}^\mathrm{T} \mathbf{X}\right)^{-1}$ exists, we do not assume that $\mathbf{X}$ has any well defined inverse.   Indeed,
if $p\neq n$, then $\mathbf{X}$ will not even be square.

Let us define the following matrix $\mathbf{A}\triangleq \left( \mathbf{X}^\mathrm{T} \mathbf{X}\right) \in \mathbb{R}^{p \times p}$.  Then by substitution, we find
$$\begin{align}
\mathbf{X}^\dagger \mathbf{X} & = \left( \mathbf{X}^\mathrm{T} \mathbf{X}\right)^{-1} \mathbf{X}^\mathrm{T} \mathbf{X} \\
& = \mathbf{A}^{-1} \mathbf{A} \\
& = \mathbf{I} \in \mathbb{R}^{p \times p}.
\end{align}$$
by the associativity of matrix multiplication.

In particular, we have verified one of the properties of the <b>left pseudo-inverse</b>.  These aren't the focus of the course, but they will come up, and it is good exposure
to be aware of these objects.  They are extremely useful in applied mathematics and statistics for some reasons we will see in upcoming lectures.
</div>

<div class="pagebreak"></div>

### Problem 2:
Recall the definition of the $TSS$,
$$TSS \triangleq \sum_{i=1}^n \left(Y_i - \overline{Y}\right)^2, $$
such that the $TSS$ is a random variable, defined as a combination of the random variables $Y, \overline{Y}$. What is the value of the expectation of the $TSS$?

<div class="solutions">
#### Solution:
This is meant to be a challenging problem, and it isn't representative of a problem you will see on the midterm <em>unless you have seen something very close to it already</em>.  To begin, we will
consider a subtituion into the definition as follows,
$$\begin{align}
TSS &= \sum_{i=1}^n \left( Y_i  - \overline{Y}\right)^2 \\
& = \sum_{i=1}^n \left(\beta_0 + \beta_1 X_i - \left[\frac{1}{n} \sum_{j=1}^n \beta_0 + \beta_1 X_j + \epsilon_j\right] \right)^2 \\
& = \sum_{i=1}^n \left(\beta_0 + \beta_1 X_i - \beta_0 - \beta_1 \overline{X} + \overline{\epsilon}\right)^2 \\
& = \sum_{i=1}^n \left( \beta_1 \left[X_i - \overline{X}\right] + \left[\epsilon_i - \overline{\epsilon}\right]\right)^2
\end{align}$$


In the above, we define $\overline{\epsilon} \triangleq \frac{1}{n} \sum_{j=1}^n \epsilon_j$ as the empirical, sample-based mean of the realized $\epsilon_j$.  
Consider the following property of $\overline{\epsilon}$,
$$\begin{align}
\mathbb{E}\left[ \overline{\epsilon}\right] &= \mathbb{E}\left[\frac{1}{n} \sum_{j=1}^n \epsilon_j\right] \\
& = \frac{1}{n} \sum_{j=1}^n \mathbb{E}\left[ \epsilon_j\right] \\
&= 0
\end{align}$$
due to the usual mean zero assumption on $\epsilon_i$.  Similarly $\mathbb{E} \left[ \epsilon_i - \overline{\epsilon}\right] = 0$.

If we treat $\beta_1, X_i, \overline{X}$ as deterministic constants, then these can be treated essentially as scalar weights for the expectation, which we may
pass through the expectation without issue.  Therefore, we consider
$$\begin{align}
\mathbb{E}\left[ -2 \left(X_i - \overline{X}\right) \left(\epsilon_i - \overline{\epsilon}\right) \right] &=  -2 \left(X_i - \overline{X}\right) \mathbb{E}\left[ \left(\epsilon_i - \overline{\epsilon}\right) \right] \\
& = 0
\end{align}$$
By the above property, and by distributing the square, we find,
$$\begin{align}
\mathbb{E}\left[ TSS\right] & = \mathbb{E}\left[ \sum_{i=1}^n \left( \beta_1 \left[X_i - \overline{X}\right] + \left[\epsilon_i - \overline{\epsilon}\right]\right)^2\right] \\
& = \beta_1^2 \sum_{i=1}^n \left( X_i - \overline{X}\right)^2 + \mathbb{E} \left[ \sum_{i=1}^n \left( \epsilon_i - \overline{\epsilon}\right)^2\right]
\end{align}$$
due to the above stated properties.

The last conceptual piece to remember here is that 
$$\begin{align}
\frac{1}{n-1}\sum_{i=1}^n \left( \epsilon_i - \overline{\epsilon}\right)^2
\end{align}$$
is an unbiased estimator for the variance of $\epsilon_j$, i.e., $\sigma^2$.  This says, in particular,
$$\begin{align}
& \mathbb{E}\left[ \frac{1}{n-1}\sum_{i=1}^n \left( \epsilon_i - \overline{\epsilon}\right)^2 \right] = \sigma^2\\ 
\Leftrightarrow & \mathbb{E} \left[ \sum_{i=1}^n \left( \epsilon_i - \overline{\epsilon}\right)^2\right] = \sigma^2 ( n-1)
\end{align}$$

This tells us that the final result can be written as
$$(n-1) \sigma^2 + \beta_1^2 \sum_{i=1}^n \left( X_i - \overline{X}\right)^2. $$
The main points to practice in this problem are to remember how we compute the sample-based variance, the sample-based mean and the definition
of the regression model; we have seen all these pieces already, the challenge is putting all of the pieces together.
</div>
