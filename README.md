## This document provides some explanation for fitting the logistic regression model using the XSB Prolog system.

The data is provided in (semicolon-delimited) DSV format.

----

It is loaded using the `load_rows/1` predicate `timestep_utilities.P`. This file also contains all the auxiliary predicates for semantically parsing the rows.

----

Logistic regression is performed by the predicate `logistic_regression/4` in the Prolog file `regression.P`. It takes three input arguments:

1. A list `X` of the lists of values of the explanatory variables;
2. A list `Y` of the corresponding values of the target variable (each of them 0 or 1);
3. The (integer) number of iterations to be performed.

The list of trained coefficients is returned as the fourth argument.

Linear regression is performed by the predicate `linear_regression/3`, which takes arguments `X` and `Y` as above and returns a list of learned coefficients.

The predicate `lin_prediction/3` takes a coefficient vector and a list of lists `X` as inputs and returns a list of prediction. These can be processed by `rss/3` to compute the residual sum of squares, which can be helpful for choosing the correct explanatory variables to include.

----

The input arguments `X` and `Y` are prepared by a predicate `disappeared_vectors/2` in `regression_input_maker`. Alternative target variables to `disappeared` such as `appeared` or `channel` are accommodated by `appeared_vectors/2` and `channel_vectors/2` respectively. The list of explanatory variables used for training is adjusted by altering the list constructed in the final line of the body of `explanatories/2`.

### TL;DR

After starting XSB, the logistic regression model can be fitted by calling

```
?-  [regression,timestep_utilities,regression_input_maker],  load_rows('db_myrica_ext_complete.csv'), disappeared_vectors(X,Y), logistic_regression(X,Y,100,Coeff).
```

on the XSB command prompt.

The linear regression model can be fitted (and the residual sum of squares computed) by calling

```
[regression, timestep_utilities, regression_input_maker],  load_rows('db_myrica_ext_complete.csv'), channel_vectors(X,Y), linear_regression(X,Y,Coeff), lin_prediction(Coeff,X,YPre), rss(YPre,Y,RSS).
```
