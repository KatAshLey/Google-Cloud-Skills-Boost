<h1>gcloud Cheat Sheet</h1>

<h2>Getting Started</h2>


<h2>Help</h2>



<h2>Personalization</h2>

* `gcloud config set` defines a property for the current configuration
    * `compute/region REGION` sets the default region
    * `compute/zone ZONE_NAME` sets the default zone

<h2>Authorization and Credentials</h2>

* `gcloud auth list` lists all credentialed accounts

<h2>Projects</h2>

* `gcloud config list project` Lists project ID

<h2>IAM</h2>



<h2>Docker and Google Kubernetes Engine</h2>



<h2>Virtual Machines and Compute Engine</h2>

* `gcloud compute addresses create NAME` reserves IP addresses
    * `--global` makes addresses global
    * `--ip-version=IP_VERSION` versions of the IP address to be allocated and reserved
    * `--region REGION` specifies the region of addresses to create

* `gcloud compute addresses describe NAME` displays information about reserved static address
    * `--format=INFO` set the format for printing command output resources eg "get(address)"
    * `--global` specifies if backend is global

* `gcloud compute backend-services add-backend NAME` add a backend to a backend service
    * `--global` sets the backend as global
    * `--instance-group=INSTANCE_GROUP` name of the instance group to add to the backend service
    * `--instance-group-zone=ZONE` zone of the instance group to add ot the backend service
    * `--region=REGION` specifies the region this is created

* `gcloud compute backend-services create NAME` creates a backend system
    * `--global`
    * `--health-checks=HEALTH_CHECK` lists of health check objects for checking the health of backend service
    * `--load-balancing-scheme=LOAD_BALANCING_SCHEME` specifies the load balancer type (internal, external, internal_self_managed, external_managed or internal_managed)
    * `--port-name=PORT_NAME` specifies port instance group backends are exported to
    * `--protocol=PROTOCOL` for incoming requests refer to Google documentation

* `gcloud compute firewall-rules create FIREWALL_NAME` creates firewall rules to allow/deny incoming/outgoing traffic
    * `--action=OPTION` allow or deny. To allow or deny traffic
    * `--allow PROTOCOL:PORT` lists protocols and ports that are allowed
    * `--direction=OPTION` ingress, egress, in, out. This rule is applied to which traffic
    * `--network=default` the network the rule is attached to
    * `--source-ranges=CIDER_RANGE` list of IP address blocks that allowed to make inbound connections that match the firewall rule
    * `--rules=PROTOCOL[:PORT]` list of protocols and ports to which the firewall rule applies to
    * `--target-tags TAG_NAME` list of instance tags that the firewall rule is applied to

* `gcloud compute forwarding-rules create NAME` creates a forwarding rule to direct network traffic to a load balancer
    * `--address=ADDRESS_NAME` IP address that the forwarding rule serves
    * `--backend-service=BACKEND_SERVICE` target backend service that receives traffic
    * `--global` forwarding rule is global
    * `--load-balancing-scheme=LOAD_BALANCING_SCHEME` specifies the load balancer type (internal, external, internal_self_managed, external_managed or internal_managed) 
    * `--network= NETWorK` network that this rule applies to
    * `--ports=PORT` list of comma separated ports that packets are forwarded to
    * `--region=REGION` region of the forwarding rule
    * `--target-http-proxy=TARGET_HTTP_PROXY` target HTTP Proxy that receives the traffic
    * `--target-pool=TARGET_POOL` the target pool that receives the traffic

* `gcloud compute forwarding-rules describe NAME` displays detailed information about a forwarding rule
    * `--region REGION` region of the forwarding rule to describe

* `gcloud compute http-health-checks create http NAME` creates a HTTP health check
    * `--port PORT` TCP port number that this heath check monitors
    * `--request-path=REQUEST_PATH` the request path the health check monitors

* `gcloud compute instance list` lists instances in a project

* `gcloud compute instance-groups managed create NAME` create a compute engine managed instance group
    * `--size=NUMBER` (Required) initial number of instances
    * `--template=TEMPLATE_NAME` (Required) specifies the instance template to use
    * `--zone=ZONE` specifies the zone to create the instance group

* `gcloud compute instance-templates create NAME` creates a virtual machine instance template
    * `--image-family=debian-11` specifies the boot image
    * `--image-project=debian-cloud` image family for the operating system that the boot disk will use
    * `--machine_type=ec2-small` specifies the machine type
    * `--metadata=DETAILS`eg
        ```
        startup-script='#!/bin/bash
        apt-get update
        apt-get install apache2 -y
        a2ensite default-ssl
        a2enmod ssl
        vm_hostname="$(curl -H "Metadata-Flavor:Google" \
        http://169.254.169.254/computeMetadata/v1/instance/name)"
        echo "Page served from: $vm_hostname" | \
        tee /var/www/html/index.html
        systemctl restart apache2'
        ``` 
        information available for the operating system when its available
    * `--metadata-from-file=KEY=LOCAL_FILE_PATH` same as metadata but info from a file
    * `--network=default` specifies the network the VMs are a part of
    * `--no-address` instances are not assigned external IP addresses
    * `--region=REGION` region of the subnetwork to attach to
    * `--subnet=default` specifies the subnet the VM instance are a part of
    * `--tags=TAG_NAME` tags applied

* `gcloud compute instances create NAME` creates a virtual machine/compute engine instance
    * `--image-family=debian-11` specifies the boot image
    * `--image-project=debian-cloud` image family for the operating system that the boot disk will use
    * `--machine-type=ec2-small` specifies the machine type
    * `--metadata=DETAILS` eg
        ```
        startup-script='#!/bin/bash
        apt-get update
        apt-get install apache2 -y
        service apache2 restart
        echo "<h3>Web Server: VM_NAME</h3>" | tee /var/www/html/index.html'
        ```
        information available for the operating system when its available
    * `--tags=TAG_NAME` tags applied
    * `--zone=ZONE` zone where the instance is created

* `gcloud compute instances delete NAME` deletes instances

* `gcloud compute target-http-proxies create NAME` creates a target HTTP proxy
    * `--url-map=URL_MAP` reference to a URL map, must create url map first

* `gcloud compute target-pools add-instances NAME` adds instances to a target pool
    * `--instances INSTANCE_NAME` (Required) list instances to add to a target pool

* `gcloud compute target-pools create NAME` defines the load balanced pool of virtual machine instances
    * `--http-health-check HEALTH_CHECK_NAME` specifies the health check resource to use for this pool of instances
    * `--region REGION` region of the target pool to create

* `gcloud compute url-maps create NAME` creates a URL map
    * `--default-service=DEFAULT_SERVICE` backend service that will be used for requests

<h2>Serverless and App Engine</h2>



<h2>Miscellaneous</h2>

