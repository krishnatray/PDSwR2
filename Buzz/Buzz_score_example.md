Buzz\_score\_example.Rmd
================

Example scoring (making predictions with) the Buzz data set.

First attach the `randomForest` package and load the model and test data.

``` r
suppressPackageStartupMessages(library("randomForest"))

lst <- readRDS("thRS500.RDS")
varslist <- lst$varslist
fmodel <- lst$fmodel
buzztest <- lst$buzztest
rm(list = "lst")
```

Now show the quality of our model on held-out test data.

``` r
buzztest$prediction <- predict(fmodel, newdata = buzztest, type = "prob")[, 2, drop = TRUE]

WVPlots::ROCPlot(buzztest, "prediction", 
                 "buzz", 1, 
                 "ROC curve estimating quality of model predictions on held-out data")
```

![](Buzz_score_example_files/figure-markdown_github/unnamed-chunk-3-1.png)