# flask-app-gcp-deploy

A flask application deployed on Google Cloud Platform(GCP). Continuous deployment is coordinated with Cloud Build.  

For this project, I follewed this [YouTube Walkthrough of GCP Auto-Deploy](https://www.youtube.com/watch?v=2BJSUlaKMjQ).  

## How to use
To deploy this app on GCP and set up continuous deployment, you can follow these steps:

### Set up a project
Go to Google Cloud Platform and create a new project.  
Change your current project to this new project and activate the Cloud Shell.  
Clone this repo to your local and cd into it.  
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
Then the app is runnning locally, and you can preview this app by clicking the preview button on Cloud Shell
### Deploy this app on cloud
Configure google app engine.  
```
gcloud app deploy
```
When it asks you to choose a region, select one(in my case I select 14 us-central).  
Type "yes" when it asks whetehr you want to continue.  
Then the app is deployed on cloud, you can visit the provided url to see it.  
### Set up continuous deployment
Search Cloud Build on GCP console and open it.  
Select Trigger and create a new trigger, set repository event to "Push to a branch", connnect your related github repository as the source to watch for events, chosse master branch.  
Go to settings in Cloud Build, enable App Engine and Service accounts.  

### Done! 
Now if you make a change to your code on github, this app will be redeployed automatically. You can see the new build pipeline under Cloud Build.  
