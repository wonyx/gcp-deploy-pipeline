# gcp-deploy-pipeline

- Create two clusters
```bash
export PROJECT=$(gcloud config get-value project)
export LOCATION=asia-northeast1

export CLUSTER_1=autopilot-cluster-1
gcloud container clusters create-auto ${CLUSTER_1} \
--region ${LOCATION} \
--release-channel "regular"

export CLUSTER_2=autopilot-cluster-2
gcloud container clusters create-auto ${CLUSTER_2} \
--region ${LOCATION} \
--release-channel "regular"

```

- Create a Cloud Build Trigger:
```bash
gcloud beta builds triggers create github \
    --repo-name gcp-deploy-pipeline \
    --repo-owner wonyx \
    --branch-pattern '^main$' \
    --name gcp-deploy-pipeline \
    --build-config cloudbuild.yaml

```

- Create a Deployment Pipeline
```
gcloud deploy apply --file=clouddeploy.yaml --region=asia-northeast1
```