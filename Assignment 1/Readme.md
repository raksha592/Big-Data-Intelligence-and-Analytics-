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
