# Setup SES
prerequisite:
- a domain name
- knowledge about editing a DNS record, this guide assumes you use cloudflare to [manage your DNS](https://support.cloudflare.com/hc/en-us/articles/360019093151-Managing-DNS-records-in-Cloudflare), but it is not required, any DNS tool given by your domain provider will work as fine too.
- and, about 30 mins time

## Verify Your Domain
* [Signin to AWS console](https://console.aws.amazon.com/?nc2=h_m_mc) if you haven't done so

* Pick `Services` > `Simple Email Services`
![setup-ses-step01](img/setup-ses-step01.png)

* Pick `Domains` > `Verify a New Domain`
![setup-ses-step02](img/setup-ses-step02.png)

* In `Verify a New Domain` dialogbox, key in you domain name, check `Generate DKIM Settings` and click `Verify This Domain`
![setup-ses-step03](img/setup-ses-step03.png)

* Your DNS settings for verification will be shown on the dialogbox, keep it open, you will it it for next step
![setup-ses-step04](img/setup-ses-step04.png)

* Go to cloudflare DNS page, make sure you selected the right domain name, key in the DNS records given in previous step
> The DKIM CNAME records can not be proxied, you need to turn the orange cloud to gray cloud

![setup-ses-step05](img/setup-ses-step05.png)

* After you successfully add these CNAME records to your domain's DNS settings, Amazon SES will automatically detect the records and allow DKIM signing at that time. Verification of those records may take up to **72 hours**.

## Create Email Receiving Rule Sets
* Select `Rule Sets` > `Create a New Rule Set`
![setup-ses-step06](img/setup-ses-step06.png)

* Give your rule set a name
![setup-ses-step07](img/setup-ses-step07.png)

* Select your newly created rule set in `Inactive Rule Sets` list and click `Set as Active Rule Set`
![setup-ses-step08](img/setup-ses-step08.png)

* Click on `View Active Rule Set` button to start editing your rule set

* Click on `Create Rule` button to start adding new mailbox
![setup-ses-step09](img/setup-ses-step09.png)

### Step 1: Recipients
* add one or more email addresses as recipeints then click on `Next Step`
![setup-ses-step10](img/setup-ses-step10.png)

### Step 2: Actions
* Click `Select an action type` drop down menu, and select `S3`. click on `Next Step`
![setup-ses-step11](img/setup-ses-step11.png)

* In S3 Action Section, choose `Create S3 bucket`
![setup-ses-step12](img/setup-ses-step12.png)

* In `Create S3 bucket` dialogbox, give your bucket a name
![setup-ses-step13](img/setup-ses-step13.png)

* Leave the rest of input in S3 Action section empty and click on `Next Step`
![setup-ses-step14](img/setup-ses-step14.png)

### Step 3: Rule Details
* Give your new rule a name, and click `Next Step`
![setup-ses-step15](img/setup-ses-step15.png)

### Step 4: Review
Review your new rule settings, click `Create Rule` when you done so
![setup-ses-step16](img/setup-ses-step16.png)

Congratulations! after SES finish verifying your domain name, you can start sending mail to the email address
