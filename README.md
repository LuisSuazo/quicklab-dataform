# quicklab-dataform

## Description
Quicklab to get started in Google Cloud Dataform


## Required Tools

Setup your env in cloud shell.

```console
gcloud config set project <your_project_id>
gcloud services enable secretmanager.googleapis.com
gcloud services enable dataform.googleapis.com
PROJECT_ID=$(gcloud info --format='value(config.project)')
PROJECT_NUM=$(gcloud projects list --filter="project_id:${PROJECT_ID}"  --format='value(project_number)') 
DATAFORM_SA=service-$PROJECT_NUM@gcp-sa-dataform.iam.gserviceaccount.com
```

Create an [Github Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) to repo.
Set Up Personal Access Token with Secret Manager.

```console
for role in bigquery.jobUser bigquery.dataOwner bigquery.dataEditor secretmanager.secretAccessor; do \
    gcloud projects add-iam-policy-binding $PROJECT_ID \
    --member="serviceAccount:$DATAFORM_SA" \
    --role="roles/$role"; \
    done
```

Connect with remote repository in the dataform console.