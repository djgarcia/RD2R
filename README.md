# RD2R Ensemble

This method implements the RD2R ensemble algorithm. RD2R ensemble method is a distributed upgrade of the method present in [1].
The algorithm performs Random Discretization and Principal Components Analysis to the input data, then joins the results and trains a decision tree on it.

This software has been proved with five large real-world datasets such as:
- Poker dataset: 1M instances and 11 attributes. https://archive.ics.uci.edu/ml/datasets/Poker+Hand
- SUSY dataset: 5M instances and 18 attributes. https://archive.ics.uci.edu/ml/datasets/SUSY
- HIGGS dataset: 11M instances and 28 attributes. https://archive.ics.uci.edu/ml/datasets/HIGGS
- Epsilon dataset: 400K instances and 2K attributes. http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#epsilon
- A dataset selected for the GECCO-2014 in Vancouver, July 13th, 2014 competition, which comes from the Protein Structure Prediction field (http://cruncher.ncl.ac.uk/bdcomp/).
We have created an oversampling version of this dataset with 65 million instances, 631 attributes and 2 classes.

## Brief benchmark results:

* We outperform the original proposal and Random Forest implementation in MLlib for all datasets.
* For epsilon dataset, we have outperformed the results of Random Forest by 5% less error with just 10 trees, compared to a Random Forest with up to 500 trees.


## Example


```scala
import org.apache.spark.mllib.tree._

val nTrees = 10
val nBins = 5

// Data must be cached in order to improve the performance

val rd2rModel = RD2R.train(trainingData, // RDD[LabeledPoint]
                            nTrees, // size of the ensemble
                            nBins) // number of thresholds by feature

val predicted = rd2rModel.test(testData) // RDD[LabeledPoint]
```

## References

[1] A. Ahmad and G. Brown,
"Random Projection Random Discretization Ensembles - Ensembles of Linear Multivariate Decision Trees",
Knowledge and Data Engineering, IEEE Transactions on, vol. 26, pp. 1225–1239, May 2014.
