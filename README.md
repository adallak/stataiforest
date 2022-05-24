# stataiforest
Stata package to implement Isolation Forest algorithm.
For details see `iforest.sthlp`. 
To build Mata libraries run
```s
. do make_liforest
```

The toy example below illustrates the use of the commands.
We start by generating clustered data. For details, see 
`gendata.sthlp'.

```s
. gendata, n(400) p(2) type(cluster)
. mat X = r(X)
. mat Y = r(Y)
. svmat X
. svmat Y
```

Now, we implement iForest algorithm.

```s
. iforest X* ,extlevel(0) ntrees(100) samplesize(128)
```
When the true target `Y` is known, we can find the optimal threshold for prediction.

```s
. estat metric Y1
```
The result indicates that 0.5 is the optimal threshold value. We use this value
for the prediction

```s
. predict Yhat, threshold(0.5)
```

We can also evaluate the performance of the algorithm by visualizing ROC.

```s
. ifroc Y1
```

