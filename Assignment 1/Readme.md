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
