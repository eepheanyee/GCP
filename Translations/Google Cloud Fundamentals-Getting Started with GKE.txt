#Google Cloud Fundamentals: Getting Started with GKE


##Overview
In this lab, you create a Google Kubernetes Engine cluster containing several containers, each containing a web server. You place a load balancer in front of the cluster and view its contents.

##Objectives
In this lab, you learn how to perform the following tasks:

	- Provision a Kubernetes cluster using Kubernetes Engine.

	- Deploy and manage Docker containers using kubectl.
	

##Steps 


1: enable the following needed APIs are (Kubernetes Engine API, Container Registry API)


	gcloud services enable container.googleapis.com
	gcloud services enable containeranalysis.googleapis.com



2: For convenience, place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE. 

	export MY_ZONE=us-central1-a

3: Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:

	gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2


4: After the cluster is created, check your installed version of Kubernetes using the kubectl version command:

	kubectl version


5: View your running nodes. 

	gcloud container node-pools list --cluster=webfrontend --zone us-central1-a


6: From your Cloud Shell prompt, launch a single instance of the nginx container. (Nginx is a popular web server.)

	kubectl create deploy nginx --image=nginx:1.17.10


7: View the pod running the nginx container:

	kubectl get pods

8: Expose the nginx container to the Internet:

	kubectl expose deployment nginx --port 80 --type LoadBalancer


9: View the new service:

	kubectl get services


10: Copy your cluster's external IP address and Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.

11: Scale up the number of pods running on your service:

	kubectl scale deployment nginx --replicas 3


12: Confirm that Kubernetes has updated the number of pods:

	kubectl get pods

13: Confirm that your external IP address has not changed:

	kubectl get services

14: Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.


Thanks!
