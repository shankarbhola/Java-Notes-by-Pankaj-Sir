**Image integration**

* go to aws and create a free account
* after account creation search `s3` in the search box

![alt text](https://i.ibb.co/59W1ZRR/image.png)

* then create a bucket

![alt text](https://i.ibb.co/30b96vX/image.png)

* Name the bucket unique , that no one use this name in globally

![alt text](https://i.ibb.co/LJvb64j/image.png)

* uncheck `block all public access` , because anyone can see the images 

![alt text](https://i.ibb.co/zQ8Y6bF/image.png)

* enable `bucket versioning` , because if it is enable , if we upload the same file it will override the file, if it is disable, it will create a new file and mark this file as version 2

![alt text](https://i.ibb.co/g6KZm9P/image.png)

* create bucket

![alt text](https://i.ibb.co/x5BZkmW/image.png)

Open the bucket

![alt text](https://i.ibb.co/gJwgkdn/image.png)

click on upload

![alt text](https://i.ibb.co/Hqr2WPT/image.png)

click add files then upload the image

![alt text](https://i.ibb.co/d0rVQ5w/image.png)

open the url

it will show access denied xml

![alt text](https://i.ibb.co/zsyPdfr/image.png)

edit bucket privace then add this json object

```JSON
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "PublicRead",
			"Effect": "Allow",
			"Principal": "*",
			"Action": "s3:GetObject",
			"Resource": "arn:aws:s3:::shankarbhola/*"
		}
	]
}
```

![alt text](https://i.ibb.co/fMLdzHk/image.png)

Scroll down then click on save changes

Now refresh the url it will open the image
