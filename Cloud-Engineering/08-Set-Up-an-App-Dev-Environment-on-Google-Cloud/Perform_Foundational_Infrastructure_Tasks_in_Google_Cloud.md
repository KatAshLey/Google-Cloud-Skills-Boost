<h1>Performing Foundational Infrastructure Tasks in Google Cloud</h1>
<h2>Cloud Storage: Qwik Start - Cloud Console</h2>

Using the console
* Create a storage bucket
* Upload objects to the bucket
* Create folders and subfolders in the bucket
* Make objects in a storage bucket publicly accessible

<h2>Cloud Storage: Qwik Start - CLI/SDK</h2>

Using Command Line Interface
* Create a storage bucket
* Upload objects to the bucket
* Create folders and subfolders in the bucket
* Make objects in a storage bucket publicly accessible

<h2>Cloud IAM: Qwik Start</h2>

* Assign a role to a second user
* Remove assigned roles associated with CLoud IAM

<h2>Cloud Monitoring: Qwik Start</h2>

* Monitor a Compute Engine virtual machine (VM) instance with Cloud Monitoring
* Install monitoring and logging agents for your VM

<h2>Cloud Run Functions: Qwik Start - Console</h2>

Using the console
* Create a CLoud Run function
* Deploy and test the function
* View logs

<h2>Cloud Run Functions: Qwik Start - Command Line</h2>

Using the command line
* Create a Cloud Run function
* Deploy and test the Cloud Run function
* View logs


<h2>Pub/Sub: Qwik Start - Console</h2>

Using the console
* Set up a topic to hold data
* Subscribe to a topic to access the data
* Publish and then consume messages with a pull subscriber

<h2>Pub/Sub: Qwik Start: Command Line</h2>

Using command line
* Create, delete and list Pub/Sub topics and subscriptions
* Publish messages to a topic
* How to use a pull subscriber

<h2>Pub/Sub: Qwik Start - Python</h2>

Using Python
* Learn the basics of Pub/Sub
* Create, delete and list Pub/Sub topics and subscriptions
* Publish messages to a topic
* Use a pull subscriber to output individual messages

<h2>Set Up an App Dev Environment on Google Cloud: Challenge Lab

* Create a bucket for storing the photographs
* Create a PUb/Sub topic that will be used by a Cloud Run Function you create
* Create a Cloud Run Function
* Remove the previous cloud engineer's access from the memories project

<h2>Commands used for Challenge Lab</h2>

```
gcloud config set compute/region "REGION"

gcloud config set compute/zone "ZONE"

# create bucket
gcloud storage buckets create gs://qwiklabs-gcp-03-afbd0fbc7888-bucket --location=us-east1

# create pubsub topic
gcloud pubsub topics create topic-memories-403

gcloud pubsub topics list

# create thumbnail Cloud Run Function
gcloud config set run/region REGION

mkdir memories-thumbnail-generator && cd $_

nano index.js




supplied code

const functions = require('@google-cloud/functions-framework');
const { Storage } = require('@google-cloud/storage');
const { PubSub } = require('@google-cloud/pubsub');
const sharp = require('sharp');

functions.cloudEvent('', async cloudEvent => {
  const event = cloudEvent.data;

  console.log(`Event: ${JSON.stringify(event)}`);
  console.log(`Hello ${event.bucket}`);

  const fileName = event.name;
  const bucketName = event.bucket;
  const size = "64x64";
  const bucket = new Storage().bucket(bucketName);
  const topicName = "";
  const pubsub = new PubSub();

  if (fileName.search("64x64_thumbnail") === -1) {
    // doesn't have a thumbnail, get the filename extension
    const filename_split = fileName.split('.');
    const filename_ext = filename_split[filename_split.length - 1].toLowerCase();
    const filename_without_ext = fileName.substring(0, fileName.length - filename_ext.length - 1); // fix sub string to remove the dot

    if (filename_ext === 'png' || filename_ext === 'jpg' || filename_ext === 'jpeg') {
      // only support png and jpg at this point
      console.log(`Processing Original: gs://${bucketName}/${fileName}`);
      const gcsObject = bucket.file(fileName);
      const newFilename = `${filename_without_ext}_64x64_thumbnail.${filename_ext}`;
      const gcsNewObject = bucket.file(newFilename);

      try {
        const [buffer] = await gcsObject.download();
        const resizedBuffer = await sharp(buffer)
          .resize(64, 64, {
            fit: 'inside',
            withoutEnlargement: true,
          })
          .toFormat(filename_ext)
          .toBuffer();

        await gcsNewObject.save(resizedBuffer, {
          metadata: {
            contentType: `image/${filename_ext}`,
          },
        });

        console.log(`Success: ${fileName} → ${newFilename}`);

        await pubsub
          .topic(topicName)
          .publishMessage({ data: Buffer.from(newFilename) });

        console.log(`Message published to ${topicName}`);
      } catch (err) {
        console.error(`Error: ${err}`);
      }
    } else {
      console.log(`gs://${bucketName}/${fileName} is not an image I can handle`);
    }
  } else {
    console.log(`gs://${bucketName}/${fileName} already has a thumbnail`);
  }
});








nano package.json



supplied code
{
 "name": "thumbnails",
 "version": "1.0.0",
 "description": "Create Thumbnail of uploaded image",
 "dependencies": {
   "@google-cloud/functions-framework": "^3.0.0",
   "@google-cloud/pubsub": "^2.0.0",
   "@google-cloud/storage": "^6.11.0",
   "sharp": "^0.32.1"
 },
 "devDependencies": {},
 "engines": {
   "node": ">=4.3.2"
 }
}





npm install



gcloud functions deploy memories-thumbnail-generator \
  --gen2 \
  --runtime=nodejs22 \
  --region=us-east1 \
  --source=. \
  --entry-point=memories-thumbnail-generator \
  --trigger-bucket=qwiklabs-gcp-03-afbd0fbc7888-bucket


  
gcloud functions describe nodejs-pubsub-function \
  --region=REGION 
  





*** to sort out the permissions needed

gcloud projects get-iam-policy qwiklabs-gcp-03-afbd0fbc7888 \
  --flatten="bindings[].members" \
  --filter="bindings.members:cloud-storage" \
  --format="table(bindings.role)"

 gcloud projects describe qwiklabs-gcp-03-afbd0fbc7888 \
  --format="value(projectNumber)"
764688511067

 gcloud projects add-iam-policy-binding qwiklabs-gcp-03-afbd0fbc7888 \
  --member="serviceAccount:service-764688511067@gs-project-accounts.iam.gserviceaccount.com" \

gcloud services enable eventarc.googleapis.com pubsub.googleapis.com storage.googleapis.com cloudfunctions.googleapis.com

```