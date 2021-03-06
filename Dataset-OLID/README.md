# The Offensive Language Identification Dataset (OLID)

The Offensive Language Identification Dataset (OLID) contains a collection of 14,200 annotated English tweets using an annotation model that encompasses following three levels
  - __Level A:__ Offensive language __Detection__
    - Offensive (OFF)
    - Not offensive (NOT)

  - __Level B:__ __Categorization__ of Offensive Language
    - Targeted Insult (TIN)
    - Untargeted (UNT)

  - __Level C:__ Offensive Language __Target Identification__
    - Individual (IND)
    - Group (GRP)
    - Other (OTH) - e.g., an organization, a situation, an event, or an issue
    
----------
### Distribution over category
- Dataset: __13 240 tweets__
- Columns:
  - id
  - tweet
  - subtask_a
  - subtask_b
  - subtask_c

 - __Level A__ (100% of dataset not nan)
 
|subtask_a |Total|	Percentage|
|--|--|--|		
|NOT|	8840|	0.667674|
|OFF | 4400	|0.332326|

- __Level B__(33.23% of dataset not nan)

|subtask_b|	Total	|Percentage|
|--|--|--|		
|TIN	|3876	|0.880909|
|UNT	|524|	0.119091|

- __Level C__ (29.27% of dataset not nan)


|subtask_c|	Total|	Percentage|
|--|--|--|	
|GRP	|1074|	0.277090|
|IND	|2407	|0.621001|
|OTH	|395	|0.101909|

----------


### [Benchmarks - Level A](https://arxiv.org/pdf/1902.09666.pdf)__
  - SVM
  - BiLSTM
  - CNN
  
| Model | P  NOT| R NOT| F1 NOT| | P OFF| R OFF| F1 OFF|| P AVG| R AVG| F1 AVG|| F1 Macro| 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
| SVM| 0.80| 0.92| 0.86|| 0.66| 0.43| 0.52|| 0.76| 0.78| 0.76|| 0.69|
| BiLSTM| 0.83| 0.95| 0.89|| 0.81| 0.48| 0.60|| 0.82| 0.82| 0.81|| 0.75| 
| CNN| 0.87| 0.93| 0.90|| 0.78| 0.63| 0.70|| 0.82| 0.82| 0.81|| 0.80|
| AllNOT| -| 0.00| 0.00|| 0.72| 1.00| 0.84|| 0.52| 0.72| 0.|| 0.42|
| AllOFF| 0.28| 1.00| 0.44|| -| 0.00| 0.00|| 0.08| 0.28| 0.12|| 0.22
