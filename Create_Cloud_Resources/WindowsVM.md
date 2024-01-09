#### Check if server instance is ready for an RDP connection

`gcloud compute instances get-serial-port-output instance-1`

#### Set password for logging into the RDP
`gcloud compute reset-windows-password [instance] --zone [zone] --user [username-"admin"]`