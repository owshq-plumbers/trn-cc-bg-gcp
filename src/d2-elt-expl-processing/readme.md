<p align="center">
  <a href="" rel="noopener">
    <img src="https://github.com/owshq-plumbers/trn-cc-bg-gcp/blob/main/images/day2-summary.png" alt="Project logo">
 </a>
</p>


# Summary
Here is the summary of what is going to be covered on this day.

* Munging and preparing data for analysis
* Processing data using the most powerful processing engine
* Understand the concept of Batch and Stream in a unified system
* Develop react pipelines at scale
* Build end to end pipelines using a graphical interface


### Google DataPrep
[Parte 1 - Google DataPrep](https://github.com/owshq-plumbers/trn-cc-bg-gcp/blob/main/docs/d2.1_data_prep.excalidraw.png).

- *Munging and Preparing Data using DataPrep by Trifacta*

```shell
# save files location
dataprep-staging-90c18422-2e89-4be8-ba33-5d2a4e00bf74

# location
https://clouddataprep.com/home?projectId=silver-charmer-243611

# import data
# google cloud storage & bigquery
define parameterized path
users landing zone & users BigQuery engine

# add to new flow
# build connections
type = mongodb
ip = 45.55.97.53
db = owshq
auth db = admin
user = root

type = postgres
ip = 159.89.244.91:5432
db = owshq
user = postgres

# add recipe
# search for transformations
# unnest objects into colum
users events [BigQuery]

# flow of One Way Solution
* source
mongodb = users [Users from MongoDB]
bigquery = users [Users Event from BigQuery]

* transformations
- unnest objects
- join databases

* output & actions
- running environment (trifacta photon & dataflow)
- json new file every run [gcs]

# validate job history
job 16448067

# folder
dataprep-staging-90c18422-2e89-4be8-ba33-5d2a4e00bf74
```

### Google DataProc
[Parte 2 - Google DataProc](https://github.com/owshq-plumbers/trn-cc-bg-gcp/blob/main/docs/d2.2_data_proc.excalidraw.png).

- *Deploying and Executing a PySpark App on Google DataProc ServerLess*

[Local PySpark App](https://github.com/owshq-plumbers/trn-cc-bg-gcp/blob/main/src/d2-elt-expl-processing/pyspark-yelp-elt-py/local.py)
```shell
# build local spark application
https://github.com/owshq-plumbers/trn-cc-bg-gcp/blob/main/src/d2-elt-expl-processing/pyspark-yelp-elt-py/local.py
```

[Production PySpark using Spark Serverless Engine](https://github.com/owshq-plumbers/trn-cc-bg-gcp/blob/main/src/d2-elt-expl-processing/pyspark-yelp-elt-py/py-etl-yelp-reviews.py)
```shell
# deploy on spark serverless engine
https://github.com/owshq-plumbers/trn-cc-bg-gcp/blob/main/src/d2-elt-expl-processing/pyspark-yelp-elt-py/py-etl-yelp-reviews.py
```

### Google DataFlow
[Parte 3 - Google DataFlow](https://github.com/owshq-plumbers/trn-cc-bg-gcp/blob/main/docs/d2.3_data_flow.excalidraw.png).

- *Writing a Pipeline using Python on Google DataFlow*

```shell
# python sdk
https://beam.apache.org/documentation/sdks/python/
https://beam.apache.org/releases/pydoc/current/

# env validation
python --version
python 3.9.15

pip --version
pip 21.1.2 from /Users/luanmorenomaciel/GitHub/trn-cc-bg-gcp/venv/lib/python3.9/site-packages/pip (python 3.9)

# examples libraries
https://github.com/apache/beam/tree/master/sdks/python/apache_beam/examples

# simulate
https://cloud.google.com/sdk/gcloud/reference/beta/emulators/

# start app 
# local runner = direct runner
/Users/luanmorenomaciel/GitHub/trn-cc-bg-gcp/src/d2-elt-expl-processing/python-beam-etl
python stream.py --runner DirectRunner 

# move to dataflow engine
 gcloud dataflow --help
 
# view info
gcloud dataflow jobs list --region us-east1    

# deploy app
python -m stream \
  --stream \
  --runner DataflowRunner \
  --project silver-charmer-243611 \
  --region us-east1 \
  --temp_location gs://owshq-dataflow-staging/ \
  --job_name dataflow-py-beam-stream-user-events

# view job
gcloud --format=json dataflow jobs describe 2022-11-08_09_12_44-6400260458855607177 --region us-east1

# delete streaming job [cancel]
gcloud dataflow jobs cancel 2022-11-08_09_12_44-6400260458855607177 --region us-east1    
```

```sql
SELECT COUNT(*)
FROM `silver-charmer-243611.OneWaySolution.enriched-user-events` LIMIT 1000

SELECT *
FROM `silver-charmer-243611.OneWaySolution.enriched-user-events` LIMIT 1000
```

### Google Cloud Functions
[Parte 4 - Google Cloud Functions](https://github.com/owshq-plumbers/trn-cc-bg-gcp/blob/main/docs/d2.4_cloud_functions.excalidraw.png).

- *Building a Reactive Metadata Pipeline using Python Provider*

```shell
# specification to describe event data
https://cloudevents.io/

# functions framework for python
# write lightweight functions that run in many different environments
# cloud functions, local, cloud run, anthos
# knative envs
https://github.com/GoogleCloudPlatform/functions-framework-python

# samples
https://github.com/GoogleCloudPlatform/python-docs-samples/tree/main/functions

# build the cloud function using 2nd gen
https://cloud.google.com/functions/docs/concepts/version-comparison

* longer request processing times
* larger instance sizes
* improved concurrency
* traffic management
* eventarc integration [https://cloud.google.com/eventarc/docs]
* broader cloud events support [https://cloudevents.io/]

# info about the google cloud function
# https://cloud.google.com/functions/docs/samples/functions-cloudevent-storage
# https://cloud.google.com/functions/docs/tutorials/storage
# https://github.com/googleapis/google-cloudevents
name = cf-py-gcs-metadata
region = us-central1
event provider = cloud storage [eventarc]
event type = storage.buckets.create
entry point = cf-py-gcs-metadata
```


### Google Cloud Data Fusion
[Parte 5 - Google Cloud Data Fusion](https://github.com/owshq-plumbers/trn-cc-bg-gcp/blob/main/docs/d2.5_data_fusion.excalidraw.png).

- *Building Data Pipelines using Data Fusion UI*

```shell
# data fusion
name = owshq-data-fusion-development
edition = developer

```

