
# Google Cloud Fundamentals: Getting Started with Compute Engine


## Overview
In this lab, you will create virtual machines (VMs) and connect to them. You will also create connections between the instances.

## Objectives
In this lab, you will learn how to perform the following tasks:

	- Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

	- Create a Compute Engine virtual machine using the gcloud command-line interface.

	- Connect between the two instances.



## Steps


1. Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

	- Create a Compute Virtual Machine Named "my-vm-1";  in  "us-central1-a" Zone  with  "Debian GNU/Linux 9 (stretch)" boot disk image and tags "http, https"

		gcloud beta compute instances create my-vm-1 --zone=us-central1-a --machine-type=e2-medium --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE  --tags=http-server,https-server --image=debian-9-stretch-v20200910 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=my-vm-1 --reservation-affinity=any

	- Create firewalrules to allow http and https traffic on the tags "http and https"
	
		gcloud compute firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server

		gcloud compute firewall-rules create default-allow-https --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:443 --source-ranges=0.0.0.0/0 --target-tags=https-server
	

2. Create a Compute Engine virtual machine using the gcloud command-line interface.

	- To display a list of all the zones in the region to which Qwiklabs assigned you
	
		gcloud compute zones list | grep us-central1

	- Set your default zone to the one Qwiklabs assigned to you
	
	gcloud config set compute/zone us-central1-a
	
	- Create a VM instance called my-vm-2 in that zone
	
		gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"
	
	-  close the Cloud Shell
	
		exit
	
	
3. Connect between VM instances

	- Connect to my-vm-2

		gcloud compute ssh my-vm-2

	- Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network

		ping my-vm-1

	- Use the ssh command to open a command prompt on my-vm-1

		ssh my-vm-1

	- At the command prompt on my-vm-1, install the Nginx web server

		sudo apt-get install nginx-light -y

	- Use the nano text editor to add a custom message to the home page of the web server

		sudo nano /var/www/html/index.nginx-debian.html

	- Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your Seth Samuel

		Hi from Seth Samuel

	- Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.


	- Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command

		curl http://localhost/

	- To exit the command prompt on my-vm-1, execute this command:

		exit

	- To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:

		curl http://my-vm-1/

	- Copy the External IP address for my-vm-1 and paste it into the address bar of a new browser tab. You will see your web server's home page, including your custom text

		- To list your compute instances, run this command

			gcloud compute instances list --zone us-central1-a

		- Paste the copied Ip Address of my-vm-1, You will see your web server's home page, including your custom text.



Thanks!!
