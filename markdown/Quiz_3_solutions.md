# Quiz 3


## Instructions

>  Write your name at the top right.  You are to work on this quiz alone without any help 
>  from any other resource <b>except for a single $8.5 \times 11$ inch page of handwritten notes</b>.  
>  This quiz will be ungraded but must be handed in for attendance. 


## Problems:

In the following, we refer to the standard regression model,
$$Y_i = \beta_0 + \beta_1 X_i + \epsilon_i,$$
for which we assume the conditions of the Gauss-Markov theorem hold.

### Problem 1:

Assume that $X = 0$ is within the scope of the model. What is the implication for the regression model if $\beta_0$ = 0 so that the model is
$$Y_i = \beta_1 X_i + \epsilon_i?$$

How would the regression function plot on a graph?

<div class="solutions">
The type of model above has a mean response which passes through the origin $\left(0,0\right)$.  In particular, this should correspond to a scenario
in which we believe (for some physical or theoretical reason) that when $X=0$, the value of the response $Y$ should also have a mean zero.  This may
correspond to a physical law or a common sense reason in the application.  As an example, we may imagine that we are modeling the population of some
species $Y$ with respect to the level of its food supply $X$.  We have reason to believe that when there is no food available, the population would
also equal zero, or at least be random variation around zero due to migration through the study area. However, we do not in general enforce the intercept 
to equal zero except for cases when there is a precise meaning to this as above.   
</div>

### Problem 2:

What is the implication for the regression model if $\beta_1 = 0$,
so that the model is 
$$Y_i = \beta_0 + \epsilon_i?$$ 
How would the regression function plot on a graph?

<div class="solutions">
If $\beta_1=0$, then this means that we believe the response $Y$ varies irrespective of the value of the explanatory variable $X$.
That is to say, there is no linear relationship (or rather a horizontal one) between the response and the explanatory variable.  The
value for $\beta_0$ will actually just be given by the population mean in this case, and we see the signal as a random variation around the
observed mean. 

</div>

