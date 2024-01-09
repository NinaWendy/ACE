## Description

##Solution

### Steps



gcloud config set compute/region europe-west1

gcloud config set compute/zone europe-west1-c


gcloud container clusters create --machine-type=e2-medium --zone=us-central1-a nucleus-cluster

gcloud container clusters get-credentials nucleus-cluster

kubectl create deployment nucleus-deployment --image=gcr.io/google-samples/hello-app:2.0

kubectl expose deployment nucleus-deployment --type=LoadBalancer --port 8082

kubectl get service

gcloud compute instance-templates create nucleus-template \
   --region=us-central1 \
   --network=default \
   --subnet=default \
   --tags=allow-health-check \
   --machine-type=e2-medium \
   --image-family=debian-11 \
   --image-project=debian-cloud \
   --metadata=startup-script='#! /bin/bash
apt-get update
apt-get install -y nginx
service nginx start
#!/bin/bash
apt-get update
apt-get install -y nginx
service nginx start
sed -i -- "s/nginx/Google Cloud Platform - \$HOSTNAME/" /var/www/html/index.nginx-debian.html'


gcloud compute instance-groups managed create nucleus-lb-backend-group \
   --template=nucleus-template --size=2 --zone=us-central1-a


gcloud compute firewall-rules create allow-tcp-rule-333 \
  --network=default \
  --action=allow \
  --direction=ingress \
  --source-ranges=130.211.0.0/22,35.191.0.0/16 \
  --target-tags=allow-health-check \
  --rules=tcp:80


gcloud compute addresses create nucleus-lb-ipv4-1 \
  --ip-version=IPV4 \
  --global
gcloud compute addresses describe nucleus-lb-ipv4-1 \
  --format="get(address)" \
  --global

gcloud compute health-checks create http nucleus-http-basic-check \
  --port 80

gcloud compute backend-services create nucleus-web-backend-service \
  --protocol=HTTP \
  --port-name=http \
  --health-checks=nucleus-http-basic-check \
  --global

gcloud compute backend-services add-backend nucleus-web-backend-service \
  --instance-group=nucleus-lb-backend-group \
  --instance-group-zone=us-central1-a \
  --global

## URL MAP
gcloud compute url-maps create nucleus-web-map-http \
    --default-service nucleus-web-backend-service

## TARGET PROXY
gcloud compute target-http-proxies create nucleus-http-lb-proxy \
    --url-map nucleus-web-map-http

## FOWARDING RULES
gcloud compute forwarding-rules create nucleus-http-content-rule \
   --address=nucleus-lb-ipv4-1\
   --global \
   --target-http-proxy=nucleus-http-lb-proxy \
   --ports=80