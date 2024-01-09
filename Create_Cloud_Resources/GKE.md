#### Create a cluster

`gcloud container clusters create --machine-type=e2-medium --zone=ZONE lab-cluster`

#### Get authentication credentials for the cluster

`gcloud container clusters get-credentials lab-cluster`

#### Create a new Deployment

`kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0`

#### Create a Kubernetes Service

`kubectl expose deployment hello-server --type=LoadBalancer --port 8080`

#### Inspect the hello-server Service

`kubectl get service`

#### Delete cluster

`gcloud container clusters delete lab-cluster`