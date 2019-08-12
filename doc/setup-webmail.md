# Setup Webmail

### Prerequisite
- a company domain name that setup previously in [Setup KloudKonsole](doc/setup-kloudkonsole.md). for this example, it is called `test`

## Signup your users
this procedure is for your users who like to view mail from the S3 bucket

* type `https://kloudkonsole.com` in your browser address bar, click on `Login` link at top right corner
![setup-kk-step00](../img/kk/00.png)

* Click `I want to register` link
![setup-kk-step01](../img/kk/01.png)

* at registration page make sure the company name is `test` fill up the form and click `Register`
![setup-kkc-step02](../img/kkc/02.png)

* if successful, you should received the instruction to verify your email address
> you should informed your account admin about your username

![setup-kkc-step03](../img/kkc/03.png)

* this step is for account admin to verify user account. go to AWS cognito, user pool page
![setup-kkc-step04](../img/kkc/04.png)

* click on `Users and groups` then look for the username. click on the username
![setup-kkc-step05](../img/kkc/05.png)

* click on the `Confirm user` button to confirm the account
![setup-kkc-step06](../img/kkc/06.png)

* make sure the `Account Status` changed to `Enabled/CONFIRM`. Informed your user the account has been confirmed and procceed to the login process
![setup-kkc-step07](../img/kkc/07.png)

* ths step is for the registered user. go back kloudkonsole page and click on `Back to login` link
![setup-kkc-step08](../img/kkc/08.png)

* login with the same credential
![setup-kkc-step09](../img/kkc/09.png)

* when you are in kloud konsole, click on mailbox at the sidebar
![setup-kkc-step10](../img/kkc/10.png)

* wait for awhile, it depends on how large is your S3 bucket, kloudkonsole will fetch the mail and show them in mailbox
![setup-kkc-step11](../img/kkc/11.png)
