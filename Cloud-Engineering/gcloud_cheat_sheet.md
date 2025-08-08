<h1>gcloud Cheat Sheet</h1>

<h2>Getting Started</h2>


<h2>Help</h2>



<h2>Personalization</h2>

* `gcloud config set` defines a property for the current configuration
    * `compute/region REGION`
    * `compute/zone ZONE_NAME`

<h2>Authorization and Credentials</h2>

* `gcloud auth list` lists all credentialed accounts

<h2>Projects</h2>

* `gcloud config list project` Lists project ID

<h2>IAM</h2>

* `gsutil acl ch -d AllUsers:R gs://BUCKET_NAME/FILE_NAME` removes all users read permissions to the file specified

* `gsutil acl ch -u AllUsers:R gs://BUCKET_NAME/FILE_NAME` grants all users read permissions to the file specified


<h2>Docker and Google Kubernetes Engine</h2>



<h2>Pub/Sub</h2>

* `gcloud  pubsub subscriptions create` creates a subscription to a topic
    * `--topic TOPIC_NAME SUBSCRIPTION_NAME`

* `gcloud pubsub subscriptions delete SUBSCRIPTION_NAME` deletes a subscription

* `gcloud pubsub subscriptions pull SUBSCRIPTION_NAME` pulls the PubSub message from a subscription
    * `--auto-ack`
    * `--limit=NUMBER`

* `gcloud pubsub topics create TOPIC_NAME` creates a topic

* `gcloud pubsub topics delete TOPIC_NAME` deletes a topic

* `gcloud pubsub topics list` lists topics

* `gcloud pubsub topics list-subscriptions TOPIC_NAME` lists subscriptions to the topic provided

* `gcloud pubsub topics publish TOPIC_NAME`publishes a message to a topic
    * `--message "MESSAGE"`


<h2>Serverless and App Engine</h2>

* `gcloud functions describe FUNCTION_NAME` describe an attribute of a function

* `gcloud functions deploy FUNCTION_NAME` creates a Cloud Run function
    * `--gen2`
    * `--runtime=RUNTIME`
    * `--region=REGION`
    * `--source=.`
    * `--entry-point=ENTRY_POINT`
    * `--trigger-topic=TRIGGER_TOPIC`
    * `--stage-bucket=STAGE_BUCKET`
    * `--service-account=SERVICE_ACCOUNT`
    * `--allow-unauthenticated`

* `gcloud functions logs read FUNCTION_NAME` checks log history

* `gcloud pubsub topics publish NAME` invoke the pubsub
    * `--message="MESSAGE"`

<h2>Storage</h2>

* `gcloud storage buckets create gs://NAME` creates storage bucket with globally unique name. NOTE bucket naming conventions

* `gcloud storage cp -r gs://BUCKET_NAME/FILE_NAME` download file from storage bucket

* `gcloud storage cp FILE_NAME gs://BUCKET_NAME` copies a downloaded file into a storage bucket

* `gcloud storage cp FILE_NAME gs://BUCKET_NAME/FILE_NAME gs://BUCKET_NAME/FOLDER_NAME/FILE_NAME` creates folder, copies file into that folder

* `gcloud storage ls gs://BUCKET_NAME` lists bucket contents
    * `-l gs://BUCKET_NAME/FILE_NAME`

* `gcloud storage rm gs://BUCKET_NAME/FILE_NAME` deletes the file in the bucket


<h2>Virtual Machines and Compute Engine</h2>

* `gcloud compute addresses create NAME` reserves IP addresses
    * `--global`
    * `--ip-version=IP_VERSION`
    * `--region REGION`

* `gcloud compute addresses describe NAME` displays information about reserved static address
    * `--format=INFO`
    * `--global`

* `gcloud compute backend-services add-backend NAME` add a backend to a backend service
    * `--global`
    * `--instance-group=INSTANCE_GROUP`
    * `--instance-group-zone=ZONE`
    * `--region=REGION`

* `gcloud compute backend-services create NAME` creates a backend system
    * `--global`
    * `--health-checks=HEALTH_CHECK`
    * `--load-balancing-scheme=LOAD_BALANCING_SCHEME`
    * `--port-name=PORT_NAME`
    * `--protocol=PROTOCOL`

* `gcloud compute firewall-rules create FIREWALL_NAME` creates firewall rules to allow/deny incoming/outgoing traffic
    * `--action=OPTION`
    * `--allow PROTOCOL:PORT`
    * `--direction=OPTION`
    * `--network=default`
    * `--source-ranges=CIDER_RANGE`
    * `--rules=PROTOCOL[:PORT]`
    * `--target-tags TAG_NAME`

* `gcloud compute forwarding-rules create NAME`
    * `--address=ADDRESS_NAME`
    * `--backend-service=BACKEND_SERVICE`
    * `--global`
    * `--load-balancing-scheme=LOAD_BALANCING_SCHEME`
    * `--network= NETWORK`
    * `--ports=PORT`
    * `--region=REGION`
    * `--target-http-proxy=TARGET_HTTP_PROXY`
    * `--target-pool=TARGET_POOL`

* `gcloud compute forwarding-rules describe NAME` displays detailed information about a forwarding rule
    * `--region REGION`

* `gcloud compute http-health-checks create http NAME` creates a HTTP health check
    * `--port PORT`
    * `--request-path=REQUEST_PATH`

* `gcloud compute instances list` lists instances in a project

* `gcloud compute instance-groups managed create NAME` create a compute engine managed instance group
    * `--size=NUMBER`
    * `--template=TEMPLATE_NAME`
    * `--zone=ZONE`

* `gcloud compute instance-templates create NAME` creates a virtual machine instance template
    * `--image-family=debian-11`
    * `--image-project=debian-cloud`
    * `--machine_type=ec2-small`
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
    * `--metadata-from-file=KEY=LOCAL_FILE_PATH`
    * `--network=default`
    * `--no-address`
    * `--region=REGION`
    * `--subnet=default`
    * `--tags=TAG_NAME`

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
    * `--url-map=URL_MAP`

* `gcloud compute target-pools add-instances NAME` adds instances to a target pool
    * `--instances INSTANCE_NAME`

* `gcloud compute target-pools create NAME` defines the load balanced pool of virtual machine instances
    * `--http-health-check HEALTH_CHECK_NAME`
    * `--region REGION`

* `gcloud compute url-maps create NAME` creates a URL map
    * `--default-service=DEFAULT_SERVICE`

<h2>Miscellaneous</h2>

