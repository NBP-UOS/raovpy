raovpy
======

Compute a repeated measures anova in python by using R.

This package allows you to compute within-subject repeated measures
analysis of variance. It uses R (via rpy2) to do so. 

The package is tightly linked to occupy's datamat. The lm_anova 
function (which also computes Greenhouse-Geisser and Huynh-Feldt
corrections) uses datamats as input. However, the aov function 
can be used without. The difference is:

    * lm_anova -> Constructs a linear model in R and then uses Anova
                from car package to compute the appropriate statistics

    * aov -> Uses R's aov function to compute the anova


The functions are somewhat checked against SPSS. However, I only
compared one dataset which gives pretty much the same result, but
that is definetly not enough.

Documentation
-------------

Mainly in the source file. Contact me (Niklas) if you have questions.

The general idea of the package is this:
1) Set up a factor description, here a dictionary where the names are the factors and the values are the levels of a factor.
2) Take a bunch of datamats (one per subject) and filter them such that you'll get on datamat per cell of the anova. One cell is just a subset of the data where all factors are set to one of their levels. All combinations of factor levels make up the entire dataset.
3) Call a function that computes the dependent variable from the cell datamats. This happens in `lm_anova` (in the lambda function). If you want to use `lm_anova` you'll have to add an extra argument where you pass a function handle that does this. They are usually cheap functions like: `lambda x: mean(x.dependent_variable)`.


> For the anova: must the factor levels be numeric, or can they be strings? Like `{'category':['pleasant','neutral','unpleasant']}`, or must I recode these to integers?
It might work with strings. Test the filter by dict function and see if it gives the correct output. It depends on numpy. If you can have an array with strings and the `==` returns a logical index array it should work.

Copyright & License
-------------------

Copyright (C) 2012, Niklas Wilming
 
Licensed under GPLv2 or later, see http://www.gnu.org/licenses/gpl-2.0.txt
for license text.

