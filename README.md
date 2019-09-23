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
* After the installation, leave everything for default and click 'Finish'.
* This will run 'gcloud init' by default as it is the first step to perform. Incase it didn't run it manually
* You will have to login with your credentials. Once that is done you'll see your projects to choose from.
* In my case I've already created a project named 'KubeBoy', so I'll go ahead and select that. If you didn't create a Project yet go ahead and create one.
* After the gcloud setup run the below command
'''
gcloud componenets install kubectl
'''
* The above command will install Kubectl which is a tool to communicate with a Kubernetes Cluster.

```
gcloud config set compute/zone us-central1-a
```
* You should visit the Kubernetes Engine on your Project in the Google Cloud Console. This will enable the Kubernetes Engine API.
* Once your APIs are enabled you can access your GKE through gcloud.
* Notice that I'm using APIs in the above command which means that multiple APIs are enabled (Both Compute Engine and Kubernetes Engine)


'''
kubectl get nodes
kubectl get pods
'''
