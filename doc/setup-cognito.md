# Setup Cognito
You will need cognito to manage your user identity and access to your mailbox

### prerequisite:
- an email address setup in SES with sending capability
- about 30 mins time

## Create User Pool
* [Signin to AWS console](https://console.aws.amazon.com/?nc2=h_m_mc) if you haven't done so

* Pick `Services` > `Cognito`
![setup-cognito-step00](../img/cognito/00.png)

* Pick `Manage User Pools`, in next section we will deal with the identity pools
![setup-cognito-step01](../img/cognito/01.png)

* First click on `Create a user pool` button
![setup-cognito-step02](../img/cognito/02.png)

* Give a name to user pool, choose `Step throug settings`
![setup-cognito-step03](../img/cognito/03.png)

* Setup the attributes you going to collect from your users. unchecked `email`, we don't collect anything from our user
![setup-cognito-step04](../img/cognito/04.png)

* This page ask for the security settings of the password, use the default settings
![setup-cognito-step05](../img/cognito/05.png)

* In MFA nd verification page, feel free to add multi-factor authetication (MFA) to increase security of the credential. again since this for tester use only we keep it simple. if sms verification is not required, the SMS role creation can be ignored
![setup-cognito-step06](../img/cognito/06.png)

* In Message page, in `Do you want to customize your email address?` key in the email address you created in [Setup SES](../doc/setup-ses.md).
click `Yes` in `Do you want o send emails through your Amazon SES configuration?`
then clikc `Next Step` to proceed
![setup-cognito-step07](../img/cognito/07.png)

* Skip the `Add Tags` page
![setup-cognito-step08](../img/cognito/08.png)

* In devices page, choose `NO` to the `Do you want to remember your user's devices`. The settings will limit number of devices your user can login at the same time. for this exmaple, we ignored them
![setup-cognito-step09](../img/cognito/09.png)

* In `App Client` page, click the `Add an app client` link
![setup-cognito-step10](../img/cognito/10.png)

* Key in your client app name and also uncheck the `Generate client secret` (we will use client side aws sdk to access S3, hence we do not need this)
![setup-cognito-step11](../img/cognito/11.png)
![setup-cognito-step12](../img/cognito/12.png)

* Skip the `Triggers` page
![setup-cognito-step13](../img/cognito/13.png)

* In `Review` page, after reviewing the settings click on `Create pool` button to create your user pool
![setup-cognito-step14](../img/cognito/14.png)

* after creating user pool, click on `Domain name` on side bar
![setup-cognito-step14](../img/cognito/14a.png)

* Give your cognito signup and signin a domain name, click on `Check availability` make sure it is still available then click `Save changes`
![setup-cognito-step14](../img/cognito/14b.png)

### Take Away
Please take note of these two ID, they are useful in following steps
- User Pool Id: `ap-southeast-1_XXXXXXXX`
![setup-cognito-step15](../img/cognito/15.png)
- App Client Id: `xxxxxxxxxxxxxxxxxxxxxxxxxx`
![setup-cognito-step16](../img/cognito/16.png)

## Create Identity Pool
While user pool help you manage your users, identity pool manage their permission. this section discuss how to allow your regisered users to access your S3
bucket

* From User Pool page click `Federated Identities` link
![setup-cognito-step17](../img/cognito/17.png)

* Click `Create a New Identity Pool` button
![setup-cognito-step18](../img/cognito/18.png)

* give your identity pool a name, expand `Authentication providers` and key in the user pool id and app client id you noted in last section
![setup-cognito-step19](../img/cognito/19.png)

* finally click `Allow` to create two roles in IAM for your registered users. one for autenticated users and another one for unautneticated users.
![setup-cognito-step20](../img/cognito/20.png)

### Take Away
Please take note of the identity pool
![setup-cognito-step21](../img/cognito/21.png)

