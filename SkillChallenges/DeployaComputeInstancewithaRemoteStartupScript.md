## Challenge scenario

You have been given the responsibility of managing the configuration of your organization's Google Cloud virtual machines. You have decided to make some changes to the framework used for managing the deployment and configuration machines - you want to make it easier to modify the startup scripts used to initialize a number of the compute instances. Instead of storing startup scripts directly in the instances' metadata, you have decided to store the scripts in a Cloud Storage bucket and then configure the virtual machines to point to the relevant script file in the bucket.

A basic bash script that installs the Apache web server software called install-web.sh has been provided for you as a sample startup script. You can find the startup script in a public Cloud Storage bucket at gs://spls/gsp301/install-web.sh.

Configure a Linux Compute Engine instance that installs the Apache web server software using a remote startup script. In order to confirm that a compute instance Apache has successfully installed, the Compute Engine instance must be accessible via HTTP from the internet. You must create your instance in the following zone: us-east4-a.

### TASK 1
Create a storage bucket
![Alt text](/Images/1.png "bucket")

### TASK 2
Create a VM instance with a remote startup script
![Alt text](/Images/2.png "vm")
![Alt text](/Images/33.png "vm")
![Alt text](/Images/3.png "link")


### TASK 3
Create a firewall rule to allow traffic (80/tcp)
![Alt text](/Images/4.png "logs")


### TASK 4
Test that the VM is serving web content
![Alt text](/Images/5.png "webserver")


### Tips and Tricks

1. Check if your Compute Engine instance is executing the startup script. Use the Serial Console for the running virtual machine to look at the startup events to make sure that the startup script is being executed.

2. Check permissions. Your Compute Engine instance might not have the correct permissions required to read the startup script from the storage bucket. The virtual machine needs to be given permissions that align with the storage permissions.

3. Check firewalls. If the startup script has installed the software you may be unable to connect if a firewall has not been correctly configured.

4. Check the URL and address. You will be unable to connect to the Apache web server if you are trying to access the Compute Engine instance using an HTTPS address rather than HTTP; or you are using the incorrect IP address. Check that your URL is http://[EXTERNAL_IP] rather than https://[EXTERNAL_IP] or http://[INTERNAL_IP]