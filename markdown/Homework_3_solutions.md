# Homework 3 
STAT 757 -- Section 1001 <br>
Instructor: Colin Grudzien

## Due: 09/19/2019

## Instructions
<blockquote>
 You may work with others on these problems but you must turn in your own work.  
 You may type your solutions in any way you like (LaTeX, Markdown, Office, etc...) as long as you present your work clearly and in an organized way.<br>
 <strong>Whenever plotting:</strong>
<ul>
 <li> Include a copy of a short R script corresponding to your plot.</li>
 <li> Your plot must be clearly labeled in all axes, legends, and the plot must include a clear title.</li>
 <li> The plot must be sensible and easy to read. </li>
</ul>
</blockquote>

## Problems

### Problem 1:
Recall the point estimates for $\beta_0,\beta_1$ via least squares are given as,
  $$\begin{align}
  \hat{\beta}_1 &= \frac{\sum_{i=1}^n\left(X_i - \overline{X} \right)\left(Y_i - \overline{Y}\right)}{\sum_{i=1}^n\left(X_i - \overline{X} \right)^2}\\
  \hat{\beta}_0 &= \frac{1}{n} \left(\sum_{i=1}^n Y_i - \hat{\beta}_1 X_i \right) \\
  \end{align}$$
where $\overline{Y},\overline{X}$ are the means of the observed response and explanatory variables respectively.

Prove that $\hat{\beta}_0$ and $\hat{\beta}_1$ are unbiased.
<div class="solutions">
#### Solution:

We will consider the expectation of the parameter $\hat{\beta}_1$ first.
We begin by considering the substitution for $Y_i$ in terms of the regression model,
$Y_i = \beta_0 + \beta_1 X_i + \epsilon_i,$
with the goal of reducing the equation to $\beta_1$ after taking the expectation.  Specifically,

$$\begin{align}
\hat{\beta}_1 &= \frac{\sum_{i=1}^n\left(X_i - \overline{X} \right)\left(Y_i - \overline{Y}\right)}{\sum_{i=1}^n\left(X_i - \overline{X} \right)^2}\\
&= \frac{\sum_{i=1}^n\left(X_i - \overline{X} \right)\left[\beta_0 + \beta_1X_i +\epsilon_i - \frac{1}{n}\left( \sum_{i=1}^n \beta_0 + \beta_1 + \epsilon_i\right)\right]}{\sum_{i=1}^n\left(X_i
 - \overline{X} \right)^2}\\
&=\frac{\sum_{i=1}^n\left(X_i - \overline{X} \right)\left[\beta_0 + \beta_1X_i +\epsilon_i - \beta_0 -  \beta_1 \overline{X} - \overline{\epsilon}\right]}{\sum_{i=1}^n\left(X_i
 - \overline{X} \right)^2}\\
&= \frac{\sum_{i=1}^n\left(X_i - \overline{X} \right)\left[ \beta_1\left(X_i- \overline{X}\right) + \left(\epsilon_i  - \overline{\epsilon}\right)\right]}{\sum_{i=1}^n\left(X_i
 - \overline{X} \right)^2}\\
&= \frac{\sum_{i=1}^n \beta_1\left(X_i - \overline{X} \right)^2 + \left(X_i - \overline{X} \right)\left(\epsilon_i  - \overline{\epsilon}\right)}{\sum_{i=1}^n\left(X_i
 - \overline{X} \right)^2} \\
&=\beta_1 + \frac{\sum_{i=1}^n  \left(X_i - \overline{X} \right)\left(\epsilon_i  - \overline{\epsilon}\right)}{\sum_{i=1}^n\left(X_i
 - \overline{X} \right)^2}
\end{align}$$
where we define $\overline{\epsilon} = \frac{1}{n}\sum_{i=1}^n \epsilon_i$.  We recall from the last homework, we saw $\mathbb{E}\left[ \overline{\epsilon}\right]=0$, and thus the second term above is
a sum of mean zero random variables.  In the expectation we find thus,
$$\mathbb{E}\left[\hat{\beta}_1 \right] = \beta_1.$$

Given the above fact, we can consider the expectation of $\hat{\beta}_0$ directly in terms of,
$$\begin{align}
\mathbb{E}\left[\hat{\beta}_0\right] &= \mathbb{E}\left[ \frac{1}{n} \left(\sum_{i=1}^n Y_i - \hat{\beta}_1 X_i \right)\right] \\
&=  \frac{1}{n} \left(\sum_{i=1}^n \mathbb{E}\left[Y_i\right] - \left[\hat{\beta}_1 X_i\right] \right) \\
&= \frac{1}{n} \left(\sum_{i=1}^n  \beta_0 + \beta_1 X_i - \beta_1 X_i \right) \\
&= \beta_0
\end{align}$$

</div>

<div class="pagebreak"> </div>

### Problem 2:

#### Load the library "Faraway" in the R environment.  Then proceed to analyze the following data sets in this library:

<ol>
  <li> The dataset ```sat``` comes from a study entitled “Getting What You Pay For: The Debate Over Equity in Public School Expenditures.” Make a numerical and graphical summary of the data, 
  commenting on any features that you find interesting. Limit the output you present to a quantity that a busy reader would find sufficient to get a basic understanding of the data.
  </li>
  <li>  The dataset ```divusa``` contains data on divorces in the United States from 1920 to 1996. Make a numerical and graphical summary of the data as in the previous
question.
  </li>
</ol>


