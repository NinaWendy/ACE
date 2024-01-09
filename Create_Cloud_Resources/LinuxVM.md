#### Create Variables

`export REGION=REGION`
`export ZONE=$(gcloud config get-value compute/zone)`

#### Set the project region:

`gcloud config set compute/region REGION`

`gcloud config get-value compute/region`

#### Set the project zone:

`gcloud config set compute/zone ZONE`

`gcloud config get-value compute/zone`

#### create a new VM instance

`gcloud compute instances create vm1 --machine-type e2-medium --zone=$ZONE`

#### SSH into instance

`gcloud compute ssh vm1 --zone=$ZONE`

#### List firewall rules

`gcloud compute firewall-rules list`

#### Add tag to VM

`gcloud compute instances add-tags vm1 --tags http-server,https-server`

#### Update the firewall rule:

`gcloud compute firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server`

#### View system logs

`gcloud logging logs list`