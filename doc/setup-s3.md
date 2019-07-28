# Setup S3
S3 bucket by dafault does not allow communicate with third party app such as Kloud Konsole directly, this section we will discuss how to enable that

### Prerequisite
- A bucket setup in SES to receive mails, in this example it is called `mail-kloudkonsole-test`
- 30 mins time

## Set S3 Permission
* use AWS `services` shortcut to go S3 page
![setup-s3-step01](../img/s3/01.png)

* Click on `mail-kloudkonsole-test` bucket
![setup-s3-step02](../img/s3/02.png)

* Click on `Permission` tab
![setup-s3-step03](../img/s3/03.png)

* Click on `Block public access` and `edit`
![setup-s3-step04](../img/s3/04.png)

* Check `Block all public access` and click `Save` button. this can reduce the chances of accidentally share your bucket to the public
![setup-s3-step04](../img/s3/04.png)

* In the conrim dialogbox, type `confirm` and click `Confirm` button
![setup-s3-step05](../img/s3/05.png)

* While still in `Permissions` tab, click `CORS configuration` button. 
![setup-s3-step06](../img/s3/06.png)

* Paste the followCORSConfiguration to the textarea and click `Save` button
![setup-s3-step07](../img/s3/07.png)

this is to enable regstered third party app to access this bucket
```xml
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
<CORSRule>
    <AllowedOrigin>*</AllowedOrigin>
    <AllowedMethod>POST</AllowedMethod>
    <AllowedMethod>GET</AllowedMethod>
    <AllowedMethod>PUT</AllowedMethod>
    <AllowedMethod>DELETE</AllowedMethod>
    <MaxAgeSeconds>3000</MaxAgeSeconds>
    <ExposeHeader>ETag</ExposeHeader>
    <AllowedHeader>*</AllowedHeader>
</CORSRule>
</CORSConfiguration>
```

## Take Away
Please take note of the S3 bucket name and region it reside, we need these info when configure Kloud Konsole
![setup-s3-step08](../img/s3/08.png)

the region name `US East (N. Virginia)` can not be used directly, we need to get the region id from [here](https://docs.aws.amazon.com/general/latest/gr/rande.html)
![setup-s3-step09](../img/s3/09.png)

for this example 
- bucket name: `mail-kloudkonsole-test
- region: `us-east-1`
