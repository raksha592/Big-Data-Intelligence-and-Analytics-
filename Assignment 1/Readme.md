## Genetic Variant Classification

ClinVar is a public resource containing annotations about human genetic variants. 
These variants are (usually manually) classified by clinical laboratories on a categorical spectrum ranging from 
* Benign
* Likely benign 
* Uncertain significance 
* Likely pathogenic 
* Pathogenic

Some of these variants have conflicting classifications between laboratories. These variants can cause confusion when clinicians or researchers try to interpret whether the variant has an impact on the disease of a given patient.
The objective of this project is to predict whether or not a variant is likely to have a conflicting classification. Hence, this is a binary classification problem. The column class indicates if the variant has a conflicting classification. 

Conflicting classifications are when two of any of the following three categories are present for one variant, two submissions of one category are not considered conflicting.

* Likely Benign or Benign
* VUS
* Likely Pathogenic or Pathogenic

### Data Cleaning
* The dataset consists of many columns which have nearly 99% missing data. This clearly means that these columns aren't really having a big enough impact on the classification. Hence, we drop all the columns which have more that 70% of missing data.
* The column "CLNVI" has 57% missing data. from the data dictionary, we understand that the rows which are empty are the ones in which this particular variant is not present. Hence, we fill the blank rows with an string like "No variant present".
* The columns 'SIFT','PolyPhen'and 'BLOSUM62' have nearly 61% of missing data. These are mostly scores which have been calculated using prior details which we aren't aware of. For the purpose of obtaining better results in the model, we will drop these columns rather than imputing incorrect values in the missing rows.
* The rest of the columns have less than 12% missing data. Hence, we drop all the rows to obtain a clean dataset with no missing or incorrectly imputed values.

### Exploratory Data Analysis
The dataset is observed to have many columns which are categorical and have too many unique categories in each column. 
The link to EDA is provided [here](https://github.com/raksha592/Big-Data-Intelligence-and-Analytics-/blob/master/Assignment%201/Assignment%201-Part%20A-EDA.ipynb)
* For the numerical data, We observe the distributions as shown. We notice that columns like 'ORIGIN', 'CADD_PHRED', 'CADD_RAW' are likely to have outliers in the data.
* Hence we boxplot each of those columns to understand if we have outliers. We notice that the column 'ORIGIN' has an outlier when most of the data is distributed accross a particular region.
* We plot the count of categories for all the categorical columns having less than 30 categories to help us understand how the data is distributed accross the categorical data
* Next, we plot a correlation heatmap of all the columns. Since most of the columns are categorical, we are observing the correlation only between the categorical columns. A more elaborate plot of the correlation is present in the [analysis](https://github.com/raksha592/Big-Data-Intelligence-and-Analytics-/blob/master/Assignment%201/Assignment%201-Part%20B-Analysis.ipynb)
* We may visualize the stacked barplots which we group by class for some of the categorical variables like "SYMBOL", "CLNVC", "CHROM", etc to analyse how the data is distribulted accross conflicting and non-conflicting classifications

### Analysis
As mentioned previously, since most of the columns are categorical, we would have to convert them into its respective numerical forms by using techniques like one hot encoding and feature hashing
* For columns which have less than 10 categories, we one hot encode these columns
* For other categorical columns, we use a technique called "Feature hashing" and limit the number of numerical features to 5 for each of these columns
* As a result, we obtain a completely clean dataset of 113 columns
* For this analysis, we test the dataset with 3 algorithms namely 
- Logistic regression
- Decision tree classifier
- Random forest classifier
and finalise the one which gives us the most optimum result. In our case, It was random forest classifier.
