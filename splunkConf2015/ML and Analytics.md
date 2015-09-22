# Machine Learning and Analytics in Splunk

_.conf 2015_

## ML Toolkit and Showcase (App)
* https://splunkbase.splunk.com/app/2890/
* requirement: python for scientific computing app
* pre-release: not production
* limited to 50k events
* doesn't scale beyond search head to indexers or cluster

### API
* Generic grammar:

    `fit`, `apply`, `summary`
* data -> `fit` -> persistant model

    ```[training data] | fit LinearRegression metric0 into my_model costly_KPI from metric1 metric2 metric3```
* model -> `apply` -> prediction

    ```` | apply costly_KPI``` 
* summary

    ```| summary costly_KPI```

### Showcases (Dashboards)
* predict numeric fields
* predict categorical fields
* detect outliers
* forecast time series


### Splunk SPL 6.3

* `| anomolous`

## ML and Statistics

* ML: (labeled) examples -> model
* Stats: sample -> population
* E.g Face recognition
    - hard to write code from scratch
    - easy to classify examples

### Examples: 
* User behavior Analytics
* Capacity Planning
* Customer Churn

### Steps:
* log cloud storage data xfer
* clean and xform data
* build predictive model
* refine until predictions are accurate
* detect large prediction errors
* Alert / Investigate / Act
_Train the model on a different set of data_

### Stats notes:
* median absolute deviation 
    * robust because outliers don't greatly effect the deviation envelope
