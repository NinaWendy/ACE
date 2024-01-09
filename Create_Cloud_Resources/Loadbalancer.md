

#### Create VM

`gcloud compute instances create www1 \
    --zone=us-west1-c \
    --tags=network-lb-tag \
    --machine-type=e2-small \
    --image-family=debian-11 \
    --image-project=debian-cloud \
    --metadata=startup-script='#!/bin/bash
      apt-get update
      apt-get install apache2 -y
      service apache2 restart
      echo "<h3>Web Server: www1</h3>" | tee /var/www/html/index.html'`

#### Firewall rule to allow external traffic to the VM instance

`gcloud compute firewall-rules create www-firewall-network-lb \
    --target-tags network-lb-tag --allow tcp:80`

### Configure Network loadbalancer

#### Create static IP for loadbalancer

`gcloud compute addresses create network-lb-ip-1 \
  --region us-west1`

#### Add legacy HTTP health check

`gcloud compute http-health-checks create basic-check`

#### Create target pool in same region as instance

`gcloud compute target-pools create www-pool \
  --region us-west1 --http-health-check basic-check`

#### Add instance to target pool

`gcloud compute target-pools add-instances www-pool \
    --instances www1,www2,www3`

#### Add a fowarding rule

`gcloud compute forwarding-rules create www-rule \
    --region  us-west1 \
    --ports 80 \
    --address network-lb-ip-1 \
    --target-pool www-pool`

#### View the external IP address of the www-rule forwarding rule

`gcloud compute forwarding-rules describe www-rule --region us-west1`

#### Access the external IP address and Show the external IP address

`IPADDRESS=$(gcloud compute forwarding-rules describe www-rule --region us-west1 --format="json" | jq -r .IPAddress)`

`echo $IPADDRESS`

#### Send traffic to instance 

`while true; do curl -m1 $IPADDRESS; done`