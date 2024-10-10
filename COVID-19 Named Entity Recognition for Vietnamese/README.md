# COVID-19 Named Entity Recognition for Vietnamese
Finetune Qwen 2.5 0.5B on COVID-19 Named Entity Recognition for Vietnamese Dataset

# Dataset

COVID-19 Named Entity Recognition for Vietnamese Dataset is downloaded from [github](https://github.com/VinAIResearch/PhoNER_COVID19)

This dataset include 7027 training sentences and 3000 testing sentences (note that I merge train and dev dataset to have 7027 sentences). This data have input is 1 sentence and output is like of tag for each word in this sentence. This is list of entity labels: ['TRANSPORTATION', LOCATION', 'NAME' 'ORGANIZATION', 'JOB', 'GENDER', 'PATIENT_ID', 'SYMPTOM_AND_DISEASE', 'DATE', 'AGE'].

This is table number of entities:

| ENTITY               | TRAIN | TEST |
|----------------------|-------|------|
| ORGANIZATION         | 1688  | 771  |
| SYMPTOM_AND_DISEASE  | 2205  | 1136 |
| LOCATION             | 8135  | 4441 |
| DATE                 | 3652  | 1654 |
| PATIENT_ID           | 4516  | 2005 |
| AGE                  | 1043  | 582  |
| NAME                 | 537   | 318  |
| JOB                  | 337   | 173  |
| TRANSPORTATION       | 313   | 193  |
| GENDER               | 819   | 462  |

# How to use it

Just run all my notebook.

# Result and experience

You can see data, label and prediction in this file [predict.xlsx](/COVID-19 Named Entity Recognition for Vietnamese/predict.xlsx).

The model can predict correctly for 65.1% of the samples when all entities of a given input match the labels exactly. Column bugs have value True if LLM output wrong format and I can't convert back to original format.

And this is result for each labels (model only predict poorly for JOB entities, other entities type will have good results)

| Label                  | Precision | Recall  | F1-Score | Support |
|------------------------|-----------|---------|----------|---------|
| B-AGE                  | 0.9533    | 0.9124  | 0.9324   | 582     |
| B-DATE                 | 0.9829    | 0.9716  | 0.9772   | 1654    |
| B-GENDER               | 0.9404    | 0.8203  | 0.8763   | 462     |
| B-JOB                  | 0.6309    | 0.5434  | 0.5839   | 173     |
| B-LOCATION             | 0.9177    | 0.8633  | 0.8897   | 4441    |
| B-NAME                 | 0.9449    | 0.7547  | 0.8392   | 318     |
| B-ORGANIZATION         | 0.8564    | 0.8353  | 0.8457   | 771     |
| B-PATIENT_ID           | 0.9772    | 0.8349  | 0.9005   | 2005    |
| B-SYMPTOM_AND_DISEASE  | 0.9370    | 0.7861  | 0.8550   | 1136    |
| B-TRANSPORTATION       | 0.9838    | 0.9430  | 0.9630   | 193     |
| I-AGE                  | 0.4000    | 0.3333  | 0.3636   | 6       |
| I-DATE                 | 0.9854    | 0.9640  | 0.9746   | 1752    |
| I-GENDER               | 0.0000    | 0.0000  | 0.0000   | 1       |
| I-JOB                  | 0.7027    | 0.4496  | 0.5483   | 347     |
| I-LOCATION             | 0.9514    | 0.8652  | 0.9063   | 10729   |
| I-NAME                 | 0.8750    | 0.5000  | 0.6364   | 84      |
| I-ORGANIZATION         | 0.8799    | 0.8303  | 0.8544   | 3672    |
| I-PATIENT_ID           | 0.6154    | 0.2963  | 0.4000   | 27      |
| I-SYMPTOM_AND_DISEASE  | 0.9591    | 0.6957  | 0.8065   | 2156    |
| I-TRANSPORTATION       | 0.9714    | 0.9444  | 0.9577   | 72      |
| O                      | 0.9541    | 0.9902  | 0.9718   | 77773   |

| Metric          | Value   |
|-----------------|---------|
| Accuracy        | 0.9495  |
| Macro Avg       | 0.8295  |
| Weighted Avg    | 0.9489  |

We can see that Qwen 2.5 0.5B easy solved this problem. But I think we need more data for JOB entities.
