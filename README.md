## This document provides some explanation for fitting the logistic regression model using the XSB Prolog system.

To run the code in this repository, you need to install a recent version (tested with 5.0) of the XSB Prolog system, available at https://xsb.sourceforge.net/.

The instructions below assume that XSB has been started on the command line, in the main folder of the repository. 

### Replicating the analyses in the paper

After starting XSB, the logistic regression model predicting disappearance of juveniles can be fitted by calling the following command on the XSB command prompt. 

```
?-  [myricaria_germanica_ecology],  load_rows('db_myrica.csv'), disappeared_models(_,Results).
```

This returns a list of terms of the form `result(AIC,LL,Features,Coeff)`, sorted by AIC value, where the coefficients are given in the same order as the features. The final coefficient in the list is the intercept. 


The log-linear model predicting channel width can be fitted by calling the following command on the XSB command prompt. 

```
[myricaria_germanica_ecology],  load_rows('db_myrica.csv'), channel_models(_,Results).
```
or simply 
```
channel_models(_,Results).
```
if `[myricaria_germanica_ecology]` and  `load_rows('db_myrica.csv')` have already been executed in the same XSB session. 

This returns a list of terms of the form `result(AIC,RSS,Features,Coeff)`, sorted by AIC value, where the coefficients are given in the same order as the features. The final coefficient in the list is the intercept. 

### Brief explanation of the three Prolog files in this repository.


To load the code into XSB, run  `[myricaria_germanica_ecology].` from the XSB shell. 
This loads the utilities in `mg_ec_data_utilties.P` and the regression code in `regression.P` and provides a simple top-level command to perform the analyses reported in the accompanying paper. 

----

The data is provided in (semicolon-delimited) DSV format.

It is loaded using the `load_rows/1` predicate provided by `mg_ec_data_utilties.P`, which asserts it into the dynamic database. This file also contains all the auxiliary predicates for semantically parsing the rows.

----

The code performing the regression is contained in `regression.P`. 


[![DOI](https://zenodo.org/badge/1013392331.svg)](https://doi.org/10.5281/zenodo.16460618)
