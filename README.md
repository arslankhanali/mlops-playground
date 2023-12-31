# RC notes
- Rhods source(source: certified-operators) was wrong in hub file. gave errors. Rhods requires `redhat-ods-operator` namespace.
- odf app was added otherwise objectbucketclaim in mlflow app gave error. ODf when deployed correctly should create secret and config map.
- make sure to delete limitrange in credit-card-fraud project after you create the work bench in rhods. otherwise workbench gets stuck in pending state.
- With internal route INFERENCE_ENDPOINT=http://modelmesh-serving.credit-fraud-model:8008/v2/models/credit-card-fraud/infer
- With external route INFERENCE_ENDPOINT=https://credit-card-fraud-credit-fraud-model.apps.cluster-7dfg8.7dfg8.sandbox258.opentlc.com/v2/models/credit-card-fraud/infer
- For buildconfig stuff https://www.tutorialworks.com/openshift-dockerfile/
- created 2 imagestreams. one is base with python, other is resultant IS from BC.
- Should convert app deployment chart to general helm chart

```sh
# Argo password
oc get secret openshift-gitops-cluster -n openshift-gitops -o json | jq -r '.data | with_entries(.value |= @base64d)'
# MLFLOW_ROUTE value
oc get service mlflow-server -n mlops -o go-template --template='http://{{.metadata.name}}.{{.metadata.namespace}}.svc.cluster.local:8080{{println}}' 
# DATA CONNECTIONS values
oc get secrets mlflow-server -n mlops -o json | jq -r '.data.AWS_ACCESS_KEY_ID|@base64d'
oc get secrets mlflow-server -n mlops -o json | jq -r '.data.AWS_SECRET_ACCESS_KEY|@base64d'
echo "Region: us-east-2"
oc get configmap mlflow-server -n mlops -o go-template --template='http://{{.data.BUCKET_HOST}}{{println}}' 
oc get configmap mlflow-server -n mlops -o go-template --template='{{.data.BUCKET_NAME}}{{println}}' 
#
```
- endpoint needs to start with `http://`
![Alt text](images/dataconnection.png)
![Alt text](images/deploymodel.png)
- make sure path ends with `models` not `model`
![Alt text](images/modelserver.png)
![Alt text](images/Inferenceendpoint.png)
![Alt text](images/postmantest1.png)
![Alt text](images/postmantest2.png)

# Multicloud Gitops

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

[Live build status](https://validatedpatterns.io/ci/?pattern=mcgitops)

## Start Here

If you've followed a link to this repository, but are not really sure what it contains
or how to use it, head over to [Multicloud GitOps](http://hybrid-cloud-patterns.io/multicloud-gitops/)
for additional context and installation instructions
