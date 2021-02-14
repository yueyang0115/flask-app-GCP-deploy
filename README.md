# flask-app-gcp-deploy
A flask application deployed on Google Cloud Platform(GCP). Continuous deployment is coordinated with Cloud Build.  
For this project, I follewed this [YouTube Walkthrough of GCP Auto-Deploy](https://www.youtube.com/watch?v=2BJSUlaKMjQ).  
Here is a more detailed [Walkthrough](https://www.youtube.com/watch?v=_TfWdOvQXwU).

## How to use
To deploy this app on GCP and set up continuous deployment, you can follow these steps:

### Set up a project
Create a new project on GCP, change your current project to it and activate Cloud Shell.  
Create ssh-keys and upload it to Github.  
```
ssh-keygen -t rsa
```
Create a new repo on github, clone it to GCP local and cd into it.  
Create all needed files, including **app.yaml, Makefile, requirementss.txt, main.py**. The app.yaml is part of the IaC (Infrastructure as Code) and configures the PaaS environment for Google App Engine.  

### Run this app locally
Create a virtual environment and activate it.  
```
virtualenv ~/.flask
source ~/.flask/bin/activate
```
Install the required packages.  
```
make install
```
Run the application locally.
```
python main.py
```
This app will then run locally, and you can preview this app by clicking the preview button on Cloud Shell.  

### Deploy this app on cloud
(optional) Verfiy the current project is working.  
```
gcloud projects describe $GOOGLE_CLOUD_PROJECT
```
(optional) Switch your project if it's not what you want.
```
gcloud config set project $GOOGLE_CLOUD_PROJECT
```
Create app engine in cloud.  
```
gcloud app create 
```
When it asks you to choose a region, select one(in my case is 14 us-central).  
Type "yes" when it asks whetehr you want to continue.  
**Deploy this app on cloud**.  
```
gcloud app deploy
```
Then this app will be available on a public url, you can visit the provided url to see it.  

### Set up continuous deployment
Can set up CD following this [Google Cloud Tutorial](https://cloud.google.com/source-repositories/docs/quickstart-triggering-builds-with-source-repositories).  
Create **cloudbuild.yaml** file.  
Search Cloud Build on GCP console and open it.  
Select Trigger and create a new **trigger**, set repository event to "Push to a branch", connnect your related github repository as the source to watch for events, chosse master branch.  
Go to settings in Cloud Build, **enable App Engine and Service accounts**.  

### Done! See pipeline under Cloud Build
Commit all your changes to github.  
And whenever you make a new push, this app will be redeployed automatically. You can see the new build pipeline under Cloud Build.  
