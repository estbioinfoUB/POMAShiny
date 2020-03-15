
# POMA <img src='instructions/pix/logo.png' align="right" height="139" />

  <!-- badges: start -->
  
  [![Lifecycle: stable](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://www.tidyverse.org/lifecycle/#stable)
  [![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
  
  <!-- badges: end -->

This repository contains an easy-use interactive shiny app for statistical analysis of mass spectrometry data (e.g. proteomics or metabolomics). This app is based on [**POMA**](http://pcastellanoescuder.github.io/POMA/) R package and its hosted in http://polcastellano.shinyapps.io/POMA/.

## Overview  

<details><summary>CLICK HERE!</summary>

### Input Data

  - Upload your data in the *“Input Data”* tab.  
  - Data must be a .CSV *comma-separated-value* file.

**Target File**

A .CSV with two columns:

  - First/Left-hand column must be sample IDs.
  - Second/Left-hand column must be sample group/factor
    (e.g. treatment).

<img src="instructions/pix/target.png" width="60%" />

**Features File**

A .CSV with *n* columns:

  - Each row denotes a sample and each column denotes a feature.
  - First row must contain feature names.

<img src="instructions/pix/features.png" width="60%" />

**Covariates file (optional)**

A .CSV with *n* columns:

  - First/Left-hand column must be sample IDs (and must be equal than
    target file first column).
  - Each row denotes a sample (the same as in target and features files)
    and each column denotes a covariate.

<img src="instructions/pix/covariates.png" width="60%" />

-----

### Impute Values

Mass spectrometry data usually presents a high number of missing values.
By default, the missing values are treated as the result of low signal
intensity.

For this reason, the imputation of missing values is an essential step
in mass spectrometry data analysis workflow. To deal with that, POMA
provides the **Impute Value** panel which allows the user:

1.  To remove all features of the data that have more of specific
    percentage (defined by user) of missing values in ALL study groups.
    By default this parameter is 20%.

2.  To impute missing values of the data using different methods such
    as:

<!-- end list -->

  - replace by zero
  - replace by half of the minimum positive value in the original data
  - replace by median
  - replace by mean
  - replace by minimum
  - KNN method (default)

-----

### Normalization

Normalization is required to make all features comparable among them. By
default the application normalize data using *log pareto scaling*
method, however the user can compare all different methods and select
the best one according the data. POMA app offers all these following
different types of normalization methods:

  - Autoscaling
  - Level scaling
  - Log scaling
  - Log transformation
  - Vast scaling
  - Log Pareto scaling (deafult)

-----

### Visualization

Visualize your data fast and easy with POMA’s interactive boxplot and
volcano plot\!

<img src="instructions/pix/boxplots.png" width="70%" />

<img src="instructions/pix/volcano.png" width="70%" />

-----

### Statistics

The Statistical Analysis tab contains a set of different panels to
analyze the data: 1) Univariate analysis; 2) Multivariate analysis; 3)
Limma; 4) Correlation analysis; 5) Random Forest; 6) Feature selection
and 7) Rank Products. Each one of them includes different options and
methods. Below is a brief explanation of each one:

#### Univariate analysis

The Univariate Analysis panel contains four types of analysis to perform
comparaisions of each group per each feature

##### <u>Parametric tests</u>

  - T-test: The results can be shown with an interactive **volcano
    plot**.

  - One-way Analysis of Variance (ANOVA): If data has a normal
    distribution and more than two groups. <b><i>This option can be
    corrected by covariables if the user has provided a covariate
    file.</i></b>

##### <u>Non-Parametric tests</u>

  - Mann-Whitney U Test: If data has two groups and non-normal
    distribution. If data is paired, this test becomes to Wilcoxon
    Signed Rank Test.
  - Kruskal Wallis Test: If data has a non-normal distribution but more
    than two groups.

#### Multivariate analysis

This step is powered by **mixOmics R package**. POMA multivariate
analysis includes three principal multivariate methods:

  - Principal Component Analysis (PCA)

<img src="instructions/pix/pca.png" width="70%" />

  - Partial Least Squares Discriminant Analysis
(PLS-DA)

<img src="instructions/pix/plsda.png" width="70%" /><img src="instructions/pix/plsda_errors.png" width="70%" />

  - Sparse Partial Least Squares Discriminant Analysis (sPLS-DA)

<img src="instructions/pix/splsda.png" width="70%" />

#### Limma

*linear models for microarray and RNA-Seq Data*. This function is
implemented in limma R package and is prepared to perform a singl-sample
t-test using an empirical Bayes method to borrow information between
features. The final output is a list of features with a column with a
value of the contract (logFC). The AveExpr column gives the average
log2-expression level for that gene across all the arrays and channels
in the experiment. Column t is the moderated t-statistic. Column P.Value
is the associated p-value and adj.P.Value is the p-value adjusted for
multiple testing by false discovery rate (FDR).

#### Correlation analysis

The Correlation analysis tab includes two different ways to visualize
the correlations in your data.

  - Pairwise Correlation Scatterplot: This scatterplot show the
    correlation (and p-value of this correlation) between two features
    in the data. The user can choose any pair of features in the dataset
    and modify the correlation method (pearson, spearman or kendall) in
    a reactive, fast and easy panel.

<img src="instructions/pix/simple_correlations.png" width="70%" />

  - Global Correlation Heatmap: Where you can see the correlation matrix
    of your data in a heatmap format. This plot show all correlations in
    data at the same time.

<img src="instructions/pix/correlations.png" width="70%" />

#### Random Forest

Random forests or random decision forests are an ensemble learning
method for classification, regression and other tasks that operates by
constructing a multitude of decision trees. This methods are included in
the ***machine learning*** techniques.

POMA includes a Random Forest algorithm for group classification based
on **caret** R package. POMA interface allows user to tune all the
Random Forest parameters in a easy
way.

<img src="instructions/pix/tree.png" width="70%" /><img src="instructions/pix/gini.png" width="70%" />

#### Feature Selection

In statistics, feature selection, also known as variable selection, is
the process of selecting a subset of relevant features (for example,
metabolites or proteins) for use in model construction.

POMA includes a section thought specified for feature selection. This
section includes two of the most used methods for this purpose.

  - Ridge regression
  - Lasso

<img src="instructions/pix/lasso.png" width="70%" />

#### Rank Products

The rank product is a biologically motivated test for the detection of
differential features in high throughput experiments. It is a simple
**non-parametric** statistical method based on ranks of fold changes. It
can be used to combine ranked lists in various application domains,
including proteomics, statistical meta-analysis and general feature
selection.

<img src="instructions/pix/rankprod.png" width="70%" />

</details>    

## Code of Conduct  

Please note that the 'POMA' project is released with a [Contributor Code of Conduct](https://pcastellanoescuder.github.io/POMA/CODE_OF_CONDUCT.html). By contributing to this project, you agree to abide by its terms. 

