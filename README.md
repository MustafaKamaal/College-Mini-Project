# College-Mini-Project

The goal of this Project was to launch multiple containers LoadBalanced in a Kubernetes Environment.

# The Project Environment:
 This indicates the environment the Project is tested or done on
- OS = Windows
- Kubernetes Environment = Google Cloud
- Tools = gcloud, kubectl

In any Project Setting up the Environment comes first. Hence we'll set the Environment in the next few steps
In this Project we'll stick to the Command Line for the most part as it takes care of a lot of defaults

# Setting Environment
Follow the latest updated docs in the official docs as the below steps might become out of date
* Go to the [Official Docs of Google Cloud SDK](https://cloud.google.com/sdk/docs/quickstart-windows) and download the [Cloud SDK](https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe)
* Once you have downloaded the SDK, Run it.


```
gcloud config set compute/zone us-central1-a
```
