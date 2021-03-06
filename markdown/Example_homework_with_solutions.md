---
title: 'Example Homework with Solutions'
subtitle: 'STAT 757 -- Section 1001 <br> Instructor: Colin Grudzien'
---



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

#### Prove each of the following statements:
<ol>
   <li>The sum of the residuals, weighted by the corresponding predictor variable, is zero,
    $$\sum_{i=1}^n X_i \hat{\epsilon}_i = 0$$
   </li>
   <li>The sum of the residuals, weighted by the corresponding fitted value, is zero,
    $$\sum_{i=1}^n \hat{Y}_i \hat{\epsilon}_i = 0$$
   </li>
<div class="pagebreak"> </div>
   <li>The estimated regression function always passes through the point defined by the means (or the center of mass), $\left(\overline{X},\overline{Y}\right)$.
  </li>
</ol>

#### Hint: use the normal equations and the point estimates of $\hat{\beta}_0,\hat{\beta}_1$ discussed in lecture.

<div class="solutions">
#### Solution:
There are many good solutions to this problem and this one is not the only one you may use.  However, this will highlight some of the properties
that one should remember about these quantities.

Let us begin by recalling the normal equation,
$$\sum_{i=1}^n X_i Y_i = \sum_{i=1}^n \left(\hat{\beta}_0 X_i + \hat{\beta}_1 X_i^2\right).$$

Using the above fact, we will examine the equation,
$$\begin{align}
\sum_{i=1}^n X_i \hat{\epsilon}_i &= \sum_{i=1}^n X_i \left( Y_i - \hat{Y}_i \right) \\
& = \sum_{i=1}^n X_i Y_i - X_i \left(\hat{\beta}_0 + \hat{\beta}_1 X_i\right) \\
& = \sum_{i=1}^n X_i Y_i - \sum_{i=1}^n \left(\hat{\beta}_0 X_i \hat{\beta}_1 X_i^2\right) \\
& =0
\end{align}$$
by the above relationship.


Now, we will use the above relationship in the following, as well as one other relationship we showed in class,
$$\sum_{i=1}^n \hat{\epsilon}_i = 0.$$

Consider,
$$\begin{align}
\sum_{i=1}^n \hat{Y}_i \hat{\epsilon}_i = & \sum_{i=1}^n \left(\hat{\beta}_0 + \hat{\beta}_1 X_i \right) \hat{\epsilon}_i \\
& = \hat{\beta}_0 \sum_{i=1}^n \hat{\epsilon}_i + \sum_{i=1}^n X_i \hat{\epsilon}_i \\
&= 0 + 0,
\end{align}$$
by the above properties.

Finally, we will consider that,
$$Y_i = \hat{Y}_i + \hat{\epsilon}_i, $$
such that,
$$\sum_{i=1}^n Y_i = \sum_{i=1}^n \hat{Y}_i.$$
If we divide both sides by $n$, the number of cases, we obtain,
$$\overline{Y} = \frac{1}{n}\sum_{i=1}^n \hat{Y}_i .$$

But note that,
$$\begin{align}
\frac{1}{n}\sum_{i=1}^n \hat{Y}_i &= \frac{1}{n}\sum_{i=1}^n \left(\hat{\beta}_0 + \hat{\beta}_1 X_i \right) \\
& = \hat{\beta}_0 + \hat{\beta}_1 \overline{X} \\
& = \hat{Y}, 
\end{align}$$
i.e, the fitted value for the mean of the predictors $\overline{X}$ is given precisely by the mean of the observed responses.  Therefore, the estimated regression function
passes through the center of mass.
</div>


### Problem 2:

#### Install the library "Faraway" in the R environment.  Then proceed to analyze the following data sets in this library:

<ol>
  <li> The dataset ``teengamb`` concerns a study of teenage gambling in Britain. Make a numerical and graphical summary of the data, commenting on any 
  features that you find interesting. Limit the output you present to a quantity that a busy reader would find sufficient to get a basic understanding of the data.
  </li>
  <li> The dataset ``uswages`` is drawn as a sample from the Current Population Survey in 1988. Make a numerical and graphical summary of the data as in the previous
question.
  </li>
</ol>

<div class="solutions">

#### Solutions:

Problem 2 will receive full credit for completion as long as the solution satisfied the instructions.  The following are suggested ways to consider these problems, and some techniques that can help with data analysis.

</div>
```{r}
library(faraway)
library(ggplot2)
```

<div class="solutions">

##### Problem 2.1

We will plot the relationship between weekly income and gambling expenditures, but separate out the values by the reported sex.  To do this, we should convert the "sex" column into a factor vector with levels associated to the labels "Male" and "Female", which are coded as integers in the data.  We use the package "plyr" to use the function "revalue" for this purpose.

```{r}
library(plyr)
tg_sex <- as.factor(teengamb$sex)
tg_sex <- revalue(tg_sex, c("0"="Male", "1"="Female"))
teengamb$sex <- tg_sex
ggplot(data=teengamb, aes(x=income, y=gamble, color=sex)) + geom_point() + geom_smooth(method='lm') + facet_wrap(~ sex) +
  labs(
    x="Income - pounds per week",
    y="Gambling expenditure - pounds per year",
    title="Teen gambling expenditures in the UK",
    color="Sex"
  )
```

We note that when we separate out the reported sex, there is a trend between increasing income and increasing gambling expenditures for men.  However, for women the relationship between wages and gambling expenditure is basically flat.

##### Problem 2.2

As another example of changing data types, we will plot the income versus years of experience, separated out over the reported race "Black" or "White", and over the regions of surveyed individuals.  To do this, we construct a new vector called "region" from each of the existing columns "ne", "mw", "so" and "pt".  Each category is mutually exclusive, and is reported for each observation as 1 (if in this region) or 0 (if not in this region).  Therefore, we can rename these values between 1 and 4 and put these entries into a single vector as in the code below.

```{r}
usw_race <- as.factor(uswages$race)
usw_race<- revalue(usw_race, c("0"="White", "1"="Black"))
uswages$race <- usw_race
region <- uswages$ne + uswages$mw*2 + uswages$so*3 + uswages$we*4
region <- as.factor(region)
region <- revalue(region, c("1"="North East", "2"="Midwest", "3"="South", "4"="West"))
uswages$region <- region
ggplot(data=uswages, aes(x=educ, y=wage, color=race)) + geom_point() + geom_smooth(method='lm') + facet_wrap(~ region) +
  labs(
    x="Education - years",
    y="Real weekly wages in USD",
    title="Weekly US wages versus education - 1988",
    color="Race"
  )
```

Firstly we see that for individuals reported as "White", there is a slight trend between increasing education and increasing income.  This isn't uniformly the case, and this trend is expressed in part with an increasing range of income values with years of education.  However, for individuals reported as "Black", the trend between years of education and income is largely flat with a much smaller range of values for income in general.  We note that regionally, there isn't significant variation in the trends aside from the differences in reported years of education.
</div>
