<p align="center">
<img src="https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/dp3_img.png">
</p>

# Purpose:
> #### *Automating the Jenkins build and AWS Beanstalk deployment w/ Webhooks:*
> ##### Automating the build and deployment phases of a CICD pipeline will eliminate manual work and prevent human errors. We can configure a _"polling"_ setting that will check our repository at time interval that we specify. Using Webhooks, we can configure a _"trigger"_ that will send a signal to Jenkins after every new _"push"_ to our code GitHub code repository. Both methods will automatically build, test and redeploy our app, reducing our deployment time and labor cost.

##### The purpose of our app is documented here [(URL Shortener App V2)](https://github.com/djtoler/URL-Shortener___AWSBeanstalk-Jenkins#purpose)

___

# Issues:
### _1) Build failure..._

> ##### Our first build failed and our console output showed is the error pictured below. We learned that if we dont have Python and its correct version installed on our Jenkins server, Jenkins wont be able to build our app... and our pipeline will fail. 

> <p align="center">
> <img src="https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/builderror1.png">
> </p>

> ##### Jenkins depends on our machine to have the necessary Python binaries available to execute the Python code in our application. Like trying to bake a cake with no cake ingredients or baking tools. So we run the command below to give Jenkins what it needs to build our application...
> ````
> sudo apt install python3.10-venv
> ````

### _2) Webhook Payload URL Response..._
> ##### We configure a webhook in Github that will send a message to Jenkins... that will trigger Jenkins to build, test & deploy our app, everytime we push code to GitHub. In the image below, you can see that we need to enter a URL... 

> <p align="center">
> <img src="https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/webhookreqres.png">
> </p>

### On the first attempt, we entered the URL of our application for the payload URL and we got a 403 error response

| Wrong Payload URL                   | 403 Error Code                      |
| ----------------------------------- | ----------------------------------- |
| ![aaaaaa.png](https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/webhookpayloadwrong.png) | ![aaaaaa.png](https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/dp3_webhookfail.PNG) | 

### After some Google searching, we came across 2 resources that helped us understand what the payload URL is and how to structure it...
> ##### [_How to Setup a GitHub to Jenkins Pipeline with WebHooks_](https://santoshk.dev/posts/2022/how-to-setup-a-github-to-jenkins-pipeline-with-webhook/)
> ##### [_Multibranch Pipeline(With Github-webhook)_](https://blog.knoldus.com/multibranch-pipelinewith-github-webhook/)

### We found out the payload URL should be the URL of our Jenkins server, formatted like this...:
> #### Format: " http:// + address + : + port + /github-webhook/"  
> #### Example: " ht<span>tp://</span>35.153.130.215:8080/github-webhook/ "

| Correct Payload URL                   | 200 Status Code                      |
| ----------------------------------- | ----------------------------------- |
| ![aaaaaa.png](https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/webhookpayloadcorrect.png) | ![aaaaaa.png](https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/dp3_webhooksuccessres.PNG) |

___

# Steps:
## 1. [Create a new GitHub repo and download the application files from the source repo](https://github.com/djtoler/URL-Shortener-Deployment2/blob/main/Deployment2DownloadUploadFiles.md)
## 2. [Upload files to the new GitHub you created](https://github.com/djtoler/URL-Shortener-Deployment2/blob/main/UploadFilesToGitHub.md)
## 3. [Set Up Jenkins with Python on an EC2 instance & run the Jenkins Build](https://github.com/djtoler/URL-Shortener-Deployment2/blob/main/Deployment2JenkinsMarkdown.md)
## 4. [Extract the zip file that Jenkins will create](https://github.com/djtoler/URL-Shortener-Deployment2/blob/main/ExtractZipFromJenkins.md)
## 5. [Deploy the application on AWS Beanstalk](https://scribehow.com/shared/How_to_Create_and_Deploy_a_Python_URL_Shortener_on_AWS_Elastic_Beanstalk__MS9pB8lfRaGFiKAq2FU-cw) 

## We test our webhook implementation by making a visible change to our app, pushing that change to GitHub and trigger the automatic build, deploy & test in Jenkins.

> ````
> cd dp3/templates/       #Change directories into the templates folder
> nano base.html          #Open the base html file to make an edit to the body of the home page of our app
>
> #We change the background color of the home page to red the push to GitHub
> 
> git add.
> git commit -m'a commit message'
> git push
> ````

| Before push w/ Webhook                      | After push w/ Webhook                               |
| ----------------------------------- | ----------------------------------- |
| ![aaaaaa.png](https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/dp3_urlbefore.PNG) | ![aaaaaa.png](https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/redbg.PNG) |

## We can see on our Jenkins server that a build, test and deployment was automatically triggered.

> <p align="center">
> <img src="https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/autobuild.PNG">
> </p>


# System Diagram:
![dp3_diagram.png](https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/dp3_diagram.PNG)

# Optimization:

<aside>
✅ To optimize this deployment, I would add shell scripts to set up Jenkins, AWS Beanstalk and our installations to make them both run 

</aside>
