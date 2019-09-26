# College-Mini-Project

The goal of this Project was to launch multiple containers LoadBalanced in a Kubernetes Environment.

# The Project Environment:
 This indicates the environment this Project is tested or done on
- OS = Windows
- Kubernetes Environment = Google Kubernetes Engine(GKE)
- Environment = Google Cloud
- Used Services in Google Cloud = Compute Engine, GKE
- Billed for = Compute Engine Nodes - 3, Compute Engine Load Balancer - 1
- Tools = gcloud, kubectl

In this Project we'll stick to the Command Line for the most part as it takes care of a lot of defaults

# Architecture
 ![Architecture](https://github.com/MustafaKamaal/College-Mini-Project/blob/master/KubeBoy/Project.png)
 The GKE creates 3 Compute Engine Instances and forms a Kubernetes Cluster with them, while the Master is managed by the Google Cloud. On that Compute Engine Instances our Pods are Run and Load Balanced through a Compute Engine Load Balancer.
# Setting Environment
Follow the latest updated docs in the official docs as the below steps might become out of date
* Go to the [Official Docs of Google Cloud SDK](https://cloud.google.com/sdk/docs/quickstart-windows), download the [Cloud SDK](https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe) and run it.
![Installation1](https://github.com/MustafaKamaal/College-Mini-Project/blob/master/KubeBoy/Installer1.png)
* After the installation, leave everything for default and click 'Finish'.
![Installation2](https://github.com/MustafaKamaal/College-Mini-Project/blob/master/KubeBoy/Installer3.png)
* This will run 'gcloud init' by default as it is the first step to perform. Incase it didn't run it manually
```
gcloud init
```
* You will have to login with your credentials. In case you're logged in through the Browser you'll see something like this after logging and authenticating.
![Auth](https://github.com/MustafaKamaal/College-Mini-Project/blob/master/KubeBoy/auth.png)
* Once that is done you'll see your projects to choose from.
* In my case I've already created a project named 'KubeBoy', so I'll go ahead and select that. If you didn't create a Project yet go ahead and create one.
![PostInstallation](https://github.com/MustafaKamaal/College-Mini-Project/blob/master/KubeBoy/postinst1.png)
* After the gcloud setup run the below command to install Kubectl which is a tool to communicate with a Kubernetes Cluster
'''
gcloud componenets install kubectl
'''
* In the next command we'll set the default zone to 'us-central1-a'
```
gcloud config set compute/zone us-central1-a
```
* You should visit the Kubernetes Engine on your Project in the Google Cloud Console. This will enable the Kubernetes Engine API.
![APIs](https://github.com/MustafaKamaal/College-Mini-Project/blob/master/KubeBoy/api.png)
* Once your APIs are enabled you can access your GKE through gcloud.
* Notice that I'm using APIs in the above command which means that multiple APIs are enabled (Both Compute Engine and Kubernetes Engine)
## Cluster Creation and Configuration
```
gcloud container clusters create kuber
```
* The above command will create a cluster named 'kuber'. As there are a few policies for cluster naming, be sure to watch out for that
```
gcloud container clusters get-credentials kuber
```
* This will set the credetials for your Kubectl to access your Kubernetes Cluster
```
kubectl get nodes
kubectl get pods
```
* If the above commands are working and you're seeing output something similar to the below image that means you've successfully followed through till here
![Nodes](https://github.com/MustafaKamaal/College-Mini-Project/blob/master/KubeBoy/api.png)

## Load Balanced Application on Kubernetes
 Now that we've successfully Setup of Cluster and Configured it for local SDK, we will finally move on to Application Deployment.
* First we'll create a deployment named 'hello-server' with an image from Google Container Registry
```
kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
```
* Then we'll scale it to 3 pods.
```
kubectl scale --replicas=3 deployment hello-server
```
* Now, we'll finally Load Balance and expose it over the internet.
```
kubectl expose deployment hello-server --type LoadBalancer --port 80 --target-port 8080
```
* After exposing the Deployment as a service, try checking the services. You'll see a new service named 'hello-server' and external ip for it in pending state.
* Watch out for the ip with a flag -w and click 'CTRL + C' after it is up
```
kubectl get svc -w
```
![Exposing Services](https://github.com/MustafaKamaal/College-Mini-Project/blob/master/KubeBoy/exposing.png)
* This will create a service to expose the Pods through a Load Balancer
* You will see an external ip in some time and you can hit that ip to see the result
![Out](https://github.com/MustafaKamaal/College-Mini-Project/blob/master/KubeBoy/out.png)
* As there are 3 Pods, the resulting output may or may not vary as the output is hostname. If you wanna see the change try hitting the ip multiple times and you'll see the change after a few clicks.

## Deleting Everything
* Delete the Deployment
```
kubectl delete deployment hello-server
```
* Delete the Service
```
kubectl delete service hello-server
```
* Delete the Cluster
```
gcloud container clusters delete kuber
```
