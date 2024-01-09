### TASKS

1. Create a Cloud Storage bucket and place an image into it.
2. Create a Cloud SQL instance and configure it.
3. Connect to the Cloud SQL instance from a web server.
4. Use the image in the Cloud Storage bucket on a web page

#### Storage bucket
![Alt text]( "Storage bucket")

cmd1 : make a bucket named after the project ID
cmd2 : Retrieve a banner image from a publicly accessible Cloud Storage location
cmd3 : Copy the banner image to your newly created Cloud Storage bucket
cmd4 : Modify the Access Control List of the object you just created so that it's readable by everyone 

#### Cloud SQL Database
![Alt text]( "SQL DB")


Configure an application in a Compute Engine instance to use Cloud SQL

##### Steps
1. SSH into the VM instance
2. In the terminal `cd /var/www/html`
3. In the terminal `sudo nano index.php` then paste 

`<html>`

`<head><title>Welcome to my excellent blog</title></head>`

`<body>`

`<img src='https://storage.googleapis.com/qwiklabs-gcp-0005e186fa559a09/my-excellent-blog.png'>`

`<h1>Welcome to my excellent blog</h1>`

`<?php`

 `$dbserver = "CLOUDSQLIP";`

`$dbuser = "blogdbuser";`

`$dbpassword = "DBPASSWORD";`

`$conn = new mysqli($dbserver, $dbuser, $dbpassword);`

`if (mysqli_connect_error()) {`
        `echo ("Database connection failed: " . mysqli_connect_error());`
`} else {`
        `echo ("Database connection succeeded.");`
`}`

`?>`

`</body></html>`

4. `sudo service apache2 restart`