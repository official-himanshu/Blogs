# How to integrate AWS simple email service with Jenkins

![image](https://github.com/official-himanshu/Blogs/blob/master/Email-notifications-in-Jenkins.jpg)

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

###### manage Jenkins > Configure System > Email Notification 
You will see the following options under email notification section as shown in image below:

![email notification section](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2019-20-29.png)

Next we need to fill all required options in the given section to configure our email notifier.

1. SMTP Server:- First we need to add SMTP server. For this we need to go on AWS simple email dashboard and on the left side menu under Email sending section select SMTP settings. You will see the following screen which contains several information like server name, port, authentication etc.

![SMTP section](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2019-26-06.png)

2. Just copy the server name address of AWS and paste it over under SMTP server section in jenkins dashboard.
3. Next check the box of "Use SMTP authentication" and we need to provide the username and password.
4. For username and password we need to go to SES dashboard under SMTP setting and click on "Create my SMTP credentials". After that you will see a screen which asks for a username. So provide your email and click create.

![username and password](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2019-32-40.png)

5. After that you will redirect to the creditionals details and you will see here that your username and password has been created successfully. You can find your username and password under "show User SMTP Security Credentials". Just copy and paste them on jenkins email notification section.

![Username and password](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2019-33-13.png)

6. After that you will done with the username and password. Next we need to check the "SSL option on jenkins email notification section".
7. Next we need to provide the SMTP port which we find on the SMTP settings page. SMTP port may be 25, 465 and 587.
8. The next step is to provide email in "Reply-to-address" section and "UTF-8" under charset section.
9. Last we need check our email service by sending a test email. So for this check the box "Test configuration by sending test e-mail" and provide your "	Test e-mail recipient" details and send a test mail. After mail sent successfully you will check your recipient email to confirm the test email.

![full configuration](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2020-02-32.png)

10. Test email recieved look like as follows:

![ test email ](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2020-02-51.png)

This means your email notification has been successfully configured and can be used to send various email notifications in our jenkins pipeline.
After that click on save and your are done for this email configuration.

### Add email notification to your project

To allow your projects to send email you need to add “Post Build Action” and select “Email Notification” from the drop down list.

This will provide you the below interface where you can add list of email addresses to whom email is required to be sent.

![ post build action](https://github.com/official-himanshu/Blogs/blob/master/Screenshot%20from%202020-09-20%2020-15-46.png)


### Conclusion

In this blog we learn how can we configure a AWS simple email service with jenkins email notification to send email notification to various teams in our project.
If we add a post build action as a email notification so we can easily send build report and error directly to the developer and other project members involved in the project. By this we just automate the process of CI by sending details directly on their email without doing it mannually.








