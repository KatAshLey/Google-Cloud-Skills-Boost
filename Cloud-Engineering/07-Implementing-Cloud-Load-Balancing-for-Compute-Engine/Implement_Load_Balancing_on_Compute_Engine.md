<h1>Implement Load Balancing on Compute Engine</h1>

This course consists of 4 labs

<h2>Set Up Network Load Balancers</h2>

* Configure the default region and zone for your resources
* Create multiple web server instances
* Configure a load balancing service
* Configure a forwarding rule to distribute traffic

<h2>Set Up Application Load Balancers</h2>

* Configure the default region and zone for your resources
* Create an Application Load Balancer
* Test the traffic to your instances

<h2>Using an Internal Application Load Balancer</h2>

* Learn about the components that make up an Internal Load Balancer
* Create a group of backend machines (prime number calculator)
* Set up internal load balancer to direct internal traffic to the backend machines
* Test the internal load balancer from another internal machine
* Set up a public facing web server that uses the internal load balancer to get results from the internal "prime number calculator" service

<h2>Implement Load Balancing on Compute Engine: Challenge Lab</h2>

* Create multiple web server instances with firewall rules
* Configure a load balancing service
* Create an HTTP load balancer

<h2>Commands Used for Challenge Lab</h2>

```
gcloud config set compute/region us-west3


gcloud config set compute/zone us-west3-b


gcloud compute instances create web3 \
--zone=us-west3-b \
--tags=network-lb-tag \
--machine-type=e2-small \
--image-family=debian-11 \
--image-project=debian-cloud \
--metadata=startup-script='#!/bin/bash
      apt-get update
      apt-get install apache2 -y
      service apache2 restart
      echo "
<h3>Web Server: web3</h3>" | tee /var/www/html/index.html'


gcloud compute firewall-rules create www-firewall-network-lb \
--target-tags network-lb-tag --allow tcp:80


gcloud compute instances list
	
	
curl http://


gcloud compute addresses create network-lb-ip-1 \
--region=us-west3


gcloud compute http-health-checks create basic-check


gcloud compute target-pools create www-pool \
--region us-west3 --http-health-check basic-check


gcloud compute target-pools add-instances www-pool \
--instances web1,web2,web3


gcloud compute forwarding-rules create www-rule \
--region=us-west3 \
--ports=80 \
--address=network-lb-ip-1 \
--target-pool=www-pool


gcloud compute instance-templates create lb-backend-template \
--region=us-west3 \
--network=default \
--subnet=default \
--tags=allow-health-check \
--machine-type=e2-medium \
--image-family=debian-11 \
--image-project=debian-cloud \
--metadata=startup-script='#!/bin/bash
     apt-get update
     apt-get install apache2 -y
     a2ensite default-ssl
     a2enmod ssl
     vm_hostname="$(curl -H "Metadata-Flavor:Google" \
     http://169.254.169.254/computeMetadata/v1/instance/name)"
     echo "Page served from: $vm_hostname" | \
     tee /var/www/html/index.html
     systemctl restart apache2'


gcloud compute instance-groups managed create lb-backend-group \
--template=lb-backend-template --size=2 --zone=us-west3-b


gcloud compute firewall-rules create fw-allow-health-check \
--network=default \
--action=allow \
--direction=ingress \
--source-ranges=130.211.0.0/22,35.191.0.0/16 \
--target-tags=allow-health-check \
--rules=tcp:80


gcloud compute addresses create lb-ipv4-1 \
--ip-version=IPV4 \
--global


gcloud compute addresses describe lb-ipv4-1 \
--format="get(address)" \
--global


34.49.200.172


gcloud compute health-checks create http http-basic-check \
--port=80


gcloud compute backend-services create web-backend-service \
  --protocol=HTTP \
  --port-name=http \
  --health-checks=http-basic-check \
  --global
  
  
gcloud compute backend-services add-backend web-backend-service \
--instance-group=lb-backend-group \
--instance-group-zone=us-west3-b \
--global


gcloud compute url-maps create web-map-http \
--default-service web-backend-service


gcloud compute target-http-proxies create http-lb-proxy \
--url-map web-map-http


gcloud compute forwarding-rules create http-content-rule \
--address=lb-ipv4-1 \
--global \
--target-http-proxy=http-lb-proxy \
--ports=80
```