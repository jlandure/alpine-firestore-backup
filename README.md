# alpine-firestore-backup

Firestore backup image based on alpine google sdk image

# Push the image your registry

Clone this repository and launch the following command:
`git clone https://github.com/jlandure/alpine-firestore-backup.git`

Build:

`docker image build -t gcr.io/[GCLOUD_PROJECT_NAME]/alpine-firestore-backup`

Push:

`gcloud auth configure-docker`

`gcloud push gcr.io/[GCLOUD_PROJECT_NAME]/alpine-firestore-backup`

# Create a bucket on GCP

Create a [GCP coldline bucket](https://cloud.google.com/storage/docs/storage-classes) and save the name of your bucket.

# Create a service account

Create a [GCP Service account](https://cloud.google.com/iam/docs/creating-managing-service-accounts) with the following rights:

- `Owner`
- `Cloud Datastore Owner`
- `Cloud Datastore Import Export Admin`
- `Storage Admin`

Then, download the [JSON private key file](https://cloud.google.com/iam/docs/creating-managing-service-account-keys).

# Create your env variables for Cloud Run

Please refer the following information:

- `GCLOUD_PROJECT_NAME`
- `GCLOUD_BUCKET_NAME`
- `GCLOUD_SERVICE_KEY`

For the `GCLOUD_SERVICE_KEY`, please use a base64 encoded string using this command:
`cat key.json | base64`

# Set up Cloud Run

Create a Cloud Run service using your image `gcr.io/[GCLOUD_PROJECT_NAME]/alpine-firestore-backup` and set the 3 environment variables seen in the previous section.

# Launch with Cloud Scheduler

Then, prepare a Cloud Scheduler to make request to your Cloud Run Service every time you need.

For example, every Monday at 3:00am `0 3 * * 1`
