# Setup Cognito
prerequisite:
- and, about 30 mins time

## Create User Pool
* [Signin to AWS console](https://console.aws.amazon.com/?nc2=h_m_mc) if you haven't done so

* Pick `Services` > `Cognitp`
![setup-cognito-step00](img/cognito/00.png)

* Pick `Services` > `Cognitp`
![setup-cognito-step01](img/cognito/01.png)

* First click on `Manage User Pool`
![setup-cognito-step02](img/cognito/02.png)

* In `Verify a New Domain` dialogbox, key in you domain name, check `Generate DKIM Settings` and click `Verify This Domain`
![setup-cognito-step03](img/cognito/03.png)

* Your DNS settings for verification will be shown on the dialogbox, keep it open, you will it it for next step
![setup-cognito-step04](img/cognito/04.png)

* Go to cloudflare DNS page, make sure you selected the right domain name, key in the DNS records given in previous step
> The DKIM CNAME records can not be proxied, you need to turn the orange cloud to gray cloud

![setup-cognito-step05](img/cognito/05.png)

* After you successfully add these CNAME records to your domain's DNS settings, Amazon SES will automatically detect the records and allow DKIM signing at that time. Verification of those records may take up to **72 hours**.

## Create Email Receiving Rule Sets
* Select `Rule Sets` > `Create a New Rule Set`
![setup-cognito-step06](img/cognito/06.png)

* Give your rule set a name
![setup-cognito-step07](img/cognito/07.png)

* Select your newly created rule set in `Inactive Rule Sets` list and click `Set as Active Rule Set`
![setup-cognito-step08](img/cognito/08.png)

* Click on `View Active Rule Set` button to start editing your rule set

* Click on `Create Rule` button to start adding new mailbox
![setup-cognito-step09](img/cognito/09.png)

### Step 1: Recipients
* add one or more email addrescognito as recipeints then click on `Next Step`
![setup-cognito-step10](img/cognito/10.png)

### Step 2: Actions
* Click `Select an action type` drop down menu, and select `S3`. click on `Next Step`
![setup-cognito-step11](img/cognito/11.png)

* In S3 Action Section, choose `Create S3 bucket`
![setup-cognito-step12](img/cognito/12.png)

* In `Create S3 bucket` dialogbox, give your bucket a name
![setup-cognito-step13](img/cognito/13.png)

* Leave the rest of input in S3 Action section empty and click on `Next Step`
![setup-cognito-step14](img/cognito/14.png)

for more details setup process and explanation please check the [official docs](https://docs.aws.amazon.com/cognito/latest/DeveloperGuide/receiving-email.html)
