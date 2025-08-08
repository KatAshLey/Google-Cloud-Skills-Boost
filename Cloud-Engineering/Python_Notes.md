<h1>Python Notes</h1>
<h2>Pub/Sub</h2>

* `sudo apt-get install -y virtualenv` install virtual environment

* `python3 -m venv venv` builds the virtual environment

* `source venv/bin/activate` activates teh virtual environment

* `pip install --upgrade google-cloud-pubsub` installs the client library

* `git clone https://github.com/googleapis/python-pubsub.git` sample code via GitHub repository

* `cd python-pubsub/samples/snippets` navigate to a directory

* `echo $GOOGLE_CLOUD_PROJECT` shows google cloud project id details

* `cat publisher.py` view content of publisher script

* `python publisher.py -h` information about the script

* `python publisher.py $GOOGLE_CLOUD_PROJECT create TOPIC_NAME` runs script to create Pub/Sub topic

* `python publisher.py $GOOGLE_CLOUD_PROJECT list` lists all topics in a project

* `python subscriber.py $GOOGLE_CLOUD_PROJECT create TOPIC_NAME SUBSCRIPTION_NAME` creates a subscription for a topic

* `python subscriber.py $GOOGLE_CLOUD_PROJECT list-in-project` lists subscribers in a project

* `python subscriber.py -h` information about subscriber script

* `gcloud pubsub topics publish TOPIC_NAME --message "MESSAGE"` publishes a message to topic

* `python subscriber.py $GOOGLE_CLOUD_PROJECT receive SUBSCRIPTION_NAME` pulls message from topic