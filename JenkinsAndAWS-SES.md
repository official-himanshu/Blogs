# How to integrate AWS simple email service with Jenkins
Jenkins is an open source tool written in java and plugin built for continuous integration and build automation purpose.
It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery.

In this blog we are going to learn how can we integrate a AWS simple email service with jenkins default email notifier.
### Email notifier in jenkins
Jenkins provide default email notification tool which uses JavaMail for sending out e-mails. It is what comes default with Jenkins. It contains a default message containing the Build number and its status.

### Configure AWS simple email service with jenkins e-mail Notification
To integrate SES with jenkins email notifier we need to follow following steps:

#### Step 1: Login to aws account 

Firstly, visit https://aws.amazon.com/ login to our aws account console as a root user.

![ Login to aws ](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2018-21-48.png)

#### Step 2: Search for SES

Secondly, we need to go under services section on the top menu bar and search for simple email service in this section and click on that. We redirect to AWS simple email service dashboard.

![ Search simple email service](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2018-22-13.png)

#### Step 3: Verify Email

Thirdly, the most important part is to verify our e-mail which we are using for our email notification in jenkins.
For this we need to go under Identity Management on left side menu and select email addresses section on simple email dashboard. You can also verify your domain if available.

![simple email dashboard](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2018-31-57.png)

Next we need to add and verify our email in the input section provided. So for this click on "verify a new email address" option show in blue color on the SES dashboard.
After click on the option provide your email address in the pop-up input section and click on "verify this email".

![email verification](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2018-32-07.png)


After clicking on verify button a verification link is being sent to your registered email. Next we need to go to our email inbox and simple click on this link sent by AWS to verify the email.
By this our email has been verified and ready to go for our next step of configuration.

![ email verified](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2018-34-08.png)

After verification of email you show a "green verified" text in front of your email. Next we go next step to configure email notifier in jenkins.

#### Step 4: E-mail notification configuration

Next we need to go to our jenkins dashboard to configure our email notification.
After going to jenkins dashboard we need to go as follows:

###### manage Jenkins > Configure System > Email Notification you will see the following options under email notification section

![email notification section](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2019-20-29.png)




