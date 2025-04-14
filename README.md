# P
Task 1.
gcloud auth list
gcloud config list project
Task 2.
gcloud storage cp -r gs://spls/gsp290/dataflow-python-examples .
export PROJECT=
gcloud config set project $PROJECT
Task 3. 
gcloud storage buckets create gs://$PROJECT --location=REGION

gcloud storage cp gs://spls/gsp290/data_files/usa_names.csv gs://$PROJECT/data_files/
gcloud storage cp gs://spls/gsp290/data_files/head_usa_names.csv gs://$PROJECT/data_files/

Task 4. 
bq mk lake
Task 5.
cd ~
docker run -it -e PROJECT=$PROJECT -v $(pwd)/dataflow-python-examples:/dataflow python:3.8 /bin/bash

pip install apache-beam[gcp]==2.59.0
cd dataflow/
export PROJECT=
python dataflow_python_examples/data_ingestion.py \
  --project=$PROJECT \
  --region=REGION \
  --runner=DataflowRunner \
  --machine_type=e2-standard-2 \
  --staging_location=gs://$PROJECT/test \
  --temp_location gs://$PROJECT/test \
  --input gs://$PROJECT/data_files/head_usa_names.csv \
  --save_main_session
Task 6. 
python dataflow_python_examples/data_transformation.py \
  --project=$PROJECT \
  --region=REGION \
  --runner=DataflowRunner \
  --machine_type=e2-standard-2 \
  --staging_location=gs://$PROJECT/test \
  --temp_location gs://$PROJECT/test \
  --input gs://$PROJECT/data_files/head_usa_names.csv \
  --save_main_session

Task 7.
python dataflow_python_examples/data_enrichment.py \
  --project=$PROJECT \
  --region=REGION \
  --runner=DataflowRunner \
  --machine_type=e2-standard-2 \
  --staging_location=gs://$PROJECT/test \
  --temp_location gs://$PROJECT/test \
  --input gs://$PROJECT/data_files/head_usa_names.csv \
  --save_main_session
Task 8
python dataflow_python_examples/data_lake_to_mart.py \
  --worker_disk_type="compute.googleapis.com/projects//zones//diskTypes/pd-ssd" \
  --max_num_workers=4 \
  --project=$PROJECT \
  --runner=DataflowRunner \
  --machine_type=e2-standard-2 \
  --staging_location=gs://$PROJECT/test \
  --temp_location gs://$PROJECT/test \
  --save_main_session \
  --region=REGION
roject-GCP
ETL processing on GCP
