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

> ##### Jenkins depends on our machine to have the necessary Python binaries available to execute the Python code in our application. Like trying to bake a cake with no cake ingredients or baking tools. So we run the command below to give Jenkins what it needs to build our application......
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
## 1. Clone source code & set up new GH repo
> ````
> git --version
> git clone https://github.com/kura-labs-org/c4_deployment-3.git
> sudo apt install gh
> gh auth login
> gh repo create Deployment3____AWSBeanstalk_Jenkins --public
> mkdir dp3
> cp -r c4_deployment-3/* dp3/
> cd dp3/
> git init
> git add .
> git commit -m"first commit"
> git branch -M main
> git remote add origin https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins
> git push -u origin main
> cd ~
> ````

## 2. Install Jenkins
> ````
> sudo apt install openjdk-11-jdk
> apt-get update
> sudo apt-get update
> curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee     /usr/share/keyrings/jenkins-keyring.asc > /dev/null
> echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]     https://pkg.jenkins.io/debian binary/ | sudo tee     /etc/apt/sources.list.d/jenkins.list > /dev/null
> sudo apt-get update
> sudo apt-get install fontconfig openjdk-17-jre
> sudo apt-get install jenkins
> sudo systemctl start jenkins
> sudo cat /var/lib/jenkins/secrets/initialAdminPassword
> ````

## 3. Install Python, Pip and Unzip
> ````
> sudo apt update
> sudo apt install python-pip
> sudo apt install python3.10-venv
> sudo apt install unzip
> pip3 --version
> python3.10 -m venv --version
> ````

## 4. Configure Multi-Branch Jenkins Pipeline
> ````
> # Log into Jenkins server
> # Go to the dashboard
> # Click "New Item"
> # Name the project
> # Choose "Multibranch Pipeline" then "Ok"
> # Choose "Add Source" and select "GitHub"
> # Click "Add" next to _'Credentials'_
> # Add GH repo, username & use a GH token as password
> ````

## 5. Install AWS CLI
> ````
> curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
> unzip awscliv2.zip
> sudo ./aws/install
> aws --version
> aws configure
> ````

## 6. Configure Jenkins User
> ````
> sudo passwd jenkins
> sudo su - jenkins -s /bin/bash
> ````

## 7. Install AWS Beanstalk CLI
> ```
> pip install awsebcli --upgrade --user
> export PATH=$PATH:$HOME/.local/bin
> eb --version
> aws configure
> ```

## 8. Initialize & Create AWS Beanstalk Enviornment 
> ```
> cd workspace/
> ls
> cd dp3_main
> ls
> eb init
> eb create
> ```

## 9. Add Deployment Stage to Jenkins File
> ````
> Go into the Jenkins workspace and cd into our project directory.
> Add the following code snippet to our pipeline
> stage ('Deploy') { steps { sh '/var/lib/jenkins/.local/bin/eb deploy' } }
> ````

## 10. Configure Webhook
> ````
> # Log into GH
> # Open the project repo
> # Click Settings > Webhooks > Add Webhook
> # Enter payload URL
> # Select "applicaton/json"
> # Select "just the push event"
> # Click "Add Webhook"
> # Look for 200 response from the Webhook ping
> ````

## 11. Push new code to trigger automatic Jenkins build
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

---

# System Diagram:
![dp3_diagram.png](https://github.com/djtoler/Deployment3____AWSBeanstalk_Jenkins/blob/main/assets/dp3_diagram.PNG)

---

# Optimization:

<aside>
✅ To optimize this deployment, I would add shell scripts to set up Jenkins, AWS Beanstalk and our installations to make them both run 

</aside>
