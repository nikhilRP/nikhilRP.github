Last time I wrote a blog post was 3 years ago. In those 3 years lot has changed, including country I live, place I work and domain I work in.&nbsp;

After all these years of being away from this blog, I have decided to write at-least one blog post a month in the area of statistics and machine learning. My main motivation is to help out engineers and non mathematicians understand basic concepts of data science by keeping complicated math equations out of it (or to minimum).

I’ve been asked about stepwise regression recently so I thought I’d write a brief post about it.

Variable selection is probably the most common problem in regression analysis. A variable selection method is a way of selecting a particular set of independent variables for use in a regression model.
This selection might be an attempt to find a ‘best’ model, or it might be an attempt to limit the number of independent variables when there are
too many of them. There are a number of commonly used methods which we call stepwise techniques.

*   Forward selection begins with no variables selected. In the first step, it adds the most significant variable.
At each subsequent step, it adds the most significant variable of those not in the model, until there are no variables that
meet the criterion set by the user.
*   Backward selection begins with all the variables selected, and removes the least significant one at each step, until none
meet the criterion.
*   **Stepwise selection** alternates between forward and backward, bringing in and removing variables that meet the criteria
for entry or removal, until a stable set of variables is attained.
*   Bivariate screening starts by looking at all bivariate relationships with the dependent variable, and includes any that are significant in a main model

**Stepwise regression:**

The primary&nbsp;problem with stepwise regression is that we are applying methods intended for one test to many tests. In other words the assumption “single hypothesis being tested” &nbsp;is violated in ways that are difficult to determine.&nbsp;

For simplicity purposes let’s say you tossed a coin ten times and get ten heads, then
you are pretty sure that something weird is going on. You can quantify exactly how unlikely such an event is, given that the
probability of heads on any one toss is 0.5. If you have 10 people each toss a coin ten times, and one of them gets 10 heads,
you are less suspicious, but you can still quantify the likelihood. But if you have a bunch of friends (you don’t count them) toss
coins some number of times (they don’t tell you how many) and someone gets 10 heads in a row, you don’t even know how
suspicious to be. That’s stepwise.

As a result of the violation of the assumption, the following can be inferred:

*   Standard errors are biased toward 0
*   p-values also biased toward 0
*   Parameter estimates biased away from 0
*   Models too complex

This means that your parameter estimates are likely to be too far away from zero; your variance estimates for those parameter
estimates are not correct either; so confidence intervals and hypothesis tests will be wrong; and there are no reasonable ways of
correcting these problems.

The problems with Stepwise regression has been beautifully explained by Frank Harrell in the book&nbsp;[Regression Modelling
Strategies,](http://www.amazon.de/Regression-Modeling-Strategies-Applications-Statistics/dp/3319194240) and can be summarized as follows:

*   Coefficient of determination values are biased high
*   The standard errors of the parameter estimates are too small.
*   Consequently, the confidence intervals around the parameter estimates are too narrow.
*   p-values are too low, due to multiple comparisons, and are difficult to correct.
*   Parameter estimates are biased high in absolute value.
*   Collinearity problems are exacerbated

In my next blog post I will be writing about multicollinearity and how to effectively solve it.
