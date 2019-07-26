# Setup SES
You will need AWS SES to receive and send emails. SES required different configuration for incoming and outgoing email set up, therefore it is possible to have an email address that's able to receive email but unable to send out email.

### prerequisite:
- a domain name
- knowledge about editing a DNS record, this guide assumes you use cloudflare to [manage your DNS](https://support.cloudflare.com/hc/en-us/articles/360019093151-Managing-DNS-records-in-Cloudflare), but it is not required, any DNS tool given by your domain provider will work as fine too.
- and, about 30 mins time

## Verify Your Domain
* [Signin to AWS console](https://console.aws.amazon.com/?nc2=h_m_mc) if you haven't done so

* Pick `Services` > `Simple Email Services`
![setup-ses-step01](../img/ses/01.png)

* Pick `Domains` > `Verify a New Domain`
![setup-ses-step02](../img/ses/02.png)

* In `Verify a New Domain` dialogbox, key in you domain name, check `Generate DKIM Settings` and click `Verify This Domain`
![setup-ses-step03](../img/ses/03.png)

* Your DNS settings for verification will be shown on the dialogbox, keep it open, you will it it for next step
![setup-ses-step04](../img/ses/04.png)

* Go to cloudflare DNS page, make sure you selected the right domain name, key in the DNS records given in previous step
> The DKIM CNAME records can not be proxied, you need to turn the orange cloud to gray cloud

![setup-ses-step05](../img/ses/05.png)

* After you successfully add these CNAME records to your domain's DNS settings, Amazon SES will automatically detect the records and allow DKIM signing at that time. Verification of those records may take up to **72 hours**.

## Create Receiving Rule Sets
* Select `Rule Sets` > `Create a New Rule Set`
![setup-ses-step06](../img/ses/06.png)

* Give your rule set a name
![setup-ses-step07](../img/ses/07.png)

* Select your newly created rule set in `Inactive Rule Sets` list and click `Set as Active Rule Set`
![setup-ses-step08](../img/ses/08.png)

* Click on `View Active Rule Set` button to start editing your rule set

* Click on `Create Rule` button to start adding new mailbox
![setup-ses-step09](../img/ses/09.png)

### Step 1: Recipients
* add one or more email addresses as recipient then click on `Next Step`
![setup-ses-step10](../img/ses/10.png)

### Step 2: Actions
* Click `Select an action type` drop down menu, and select `S3`. click on `Next Step`
![setup-ses-step11](../img/ses/11.png)

* In S3 Action Section, choose `Create S3 bucket`
![setup-ses-step12](../img/ses/12.png)

* In `Create S3 bucket` dialogbox, give your bucket a name
![setup-ses-step13](../img/ses/13.png)

* Leave the rest of input in S3 Action section empty and click on `Next Step`
![setup-ses-step14](../img/ses/14.png)

### Step 3: Rule Details
* Give your new rule a name, and click `Next Step`
![setup-ses-step15](../img/ses/15.png)

### Step 4: Review
Review your new rule settings, click `Create Rule` when you done so
![setup-ses-step16](../img/ses/16.png)

Congratulations! after SES finish verifying your domain name, you can start sending mail to the email address

for more details setup process and explanation please check the [official docs](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/receiving-email.html)

## Create Sending Address
This step is optional to use Kloud Konsole. It is good to have email sending functionality to send out verification and welcome emails to your users. if this is not needed please feel free to skip this section.

In order to setup outgoing email address, the address must link to a mailbox first. please follow the steps in previous sections to setup incoming mailbox. for example if you want to setup `admin@example.com`, you mustsetup incoming mailbox for `admin@example.com` first.

### Verify Email Address
* click on `Email Addresses` and then `Verify a New Email Address`
![setup-ses-step17](../img/ses/17.png)

* In the popup key in your desired email address. click `Verify This Email Address` for AWS to send out verification email.
![setup-ses-step18](../img/ses/18.png)
![setup-ses-step19](../img/ses/19.png)

* go the mailbox (S3 bucket) and look for the verification mail and download it to your computer
![setup-ses-step20](../img/ses/20.png)
![setup-ses-step21](../img/ses/21.png)

* open it with any text editor and look for the email verification link, something similar to
```
https://email-verification.us-east-1.amazonaws.com/?Context=111111111111&X-Amz-Date=20190726T160834Z&Identity.IdentityName=admin%40kloudkonsole.com&X-Amz-Algorithm=AWS4-HMAC-SHA256&Identity.IdentityType=EmailAddress&X-Amz-SignedHeaders=host&X-Amz-Credential=AKIAaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaus-east-1%2Fses%2Faws4_request&Operation=ConfirmVerification&Namespace=Bacon&X-Amz-Signature=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
```

* copy the link and paste on your browser, if everything goes well you will be redirected to  the `Congratulations` page
![setup-ses-step22](../img/ses/22.png)

* go back to your SES page, you should seen the status newly added email address change to `Verified`
![setup-ses-step23](../img/ses/23.png)





