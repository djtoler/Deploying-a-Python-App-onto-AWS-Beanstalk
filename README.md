<p align="center">
<img src="https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/dp3_img.png">
</p>

# Purpose:
##### The purpose of our app is documented here (URL Shortener App V2)

  #### *Automating the Jenkins build and AWS Beanstalk deployment w/ Webhooks:*
  ##### Automating the build and deployment phases of a CICD pipeline will eliminate manual work and prevent human errors. We can configure a _"polling"_ setting that will check our repository at time interval that we specify. Using Webhooks, we can configure a _"trigger"_ that will send a signal to Jenkins after every new _"push"_ to our code GitHub code repository. Both methods will automatically build, test and redeploy our app, reducing our deployment time and labor cost.

# Issues:
### *Saving :*

##### Be sure 
````
cd /var/lib/jenkins/
````

##### In here,  
````
sudo nano config.xml
````

##### When the 

### *Installing *

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
