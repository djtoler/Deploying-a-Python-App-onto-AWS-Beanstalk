<p align="center">
<img src="https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/dp3_img.png">
</p>

# Purpose:
#### *Automating the Jenkins build and AWS Beanstalk deployment w/ Webhooks:*
  ##### Automating the build and deployment phases of a CICD pipeline will eliminate manual work and prevent human errors. We can configure a _"polling"_ setting that will check our repository at time interval that we specify. Using Webhooks, we can configure a _"trigger"_ that will send a signal to Jenkins after every new _"push"_ to our code GitHub code repository. Both methods will automatically build, test and redeploy our app, reducing our deployment time and labor cost.

  ##### The purpose of our app is documented here [(URL Shortener App V2)](https://github.com/djtoler/URL-Shortener___AWSBeanstalk-Jenkins#purpose)

___

# Issues:
### _Build failure..._

> ##### Our first build failed and our console output showed is the error pictured below. We learned that if we dont have Python and its correct version installed on our Jenkins server, Jenkins wont be able to build our app... and our pipeline will fail. 

> <p align="center">
> <img src="https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/builderror1.png">
> </p>

> ##### Jenkins depends on our machine to have the necessary Python binaries available to execute the Python code in our application. Like trying to bake a cake with no cake ingredients or baking tools. So we run the command below to give Jenkins what it needs to build our application...
> ````
> sudo apt install python3.10-venv
> ````

### _Webhook Payload URL Response..._

> <p align="center">
> <img src="https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/webhookreqres.png">
> </p>

##### Be sure 

### *Sending *

##### Make sure 

# Steps:
## 1. [Create a new GitHub repo and download the application files from the source repo](https://github.com/djtoler/URL-Shortener-Deployment2/blob/main/Deployment2DownloadUploadFiles.md)
## 2. [Upload files to the new GitHub you created](https://github.com/djtoler/URL-Shortener-Deployment2/blob/main/UploadFilesToGitHub.md)
## 3. [Set Up Jenkins with Python on an EC2 instance & run the Jenkins Build](https://github.com/djtoler/URL-Shortener-Deployment2/blob/main/Deployment2JenkinsMarkdown.md)
## 4. [Extract the zip file that Jenkins will create](https://github.com/djtoler/URL-Shortener-Deployment2/blob/main/ExtractZipFromJenkins.md)
## 5. [Deploy the application on AWS Beanstalk](https://scribehow.com/shared/How_to_Create_and_Deploy_a_Python_URL_Shortener_on_AWS_Elastic_Beanstalk__MS9pB8lfRaGFiKAq2FU-cw) 

## Automated version of Jenkins build and AWS Beanstalk deployment .
| Before Webhook                      | After Webhook                               |
| ----------------------------------- | ----------------------------------- |
| ![aaaaaa.png]() | ![aaaaaa.png]() |

# System Diagram:
![dp3_diagram.png]()

# Optimization:
<aside>
✅ To optimize this deployment, I would... 

</aside>
