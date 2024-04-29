# Continuous Integration and Continuous Delivery/Deployment(CI/CD)
**Continuous Integration (CI):** This is the practice of frequently integrating code changes into a shared repository, ideally several times a day. Each integration is automatically verified by building the project and running automated tests. This helps to catch and fix errors quickly, maintain a high quality of code, and speed up the software development process.

**Continuous Delivery (CD):** This extends CI by automatically deploying all code changes to a testing or staging environment after the build stage. The aim is to have a codebase that is always in a deployable state, allowing teams to release new changes to customers quickly and safely at any time.

**Continuous Deployment (another CD):** This goes one step further than Continuous Delivery. Every change that passes through all the stages of your production pipeline is released to customers without manual intervention. The difference between Continuous Delivery and Continuous Deployment is mainly the automatic release to production.

![preview](Images/jenkins2.png)
![preview](Images/jenkins3.png)

CI/CD Tools:
------------
1. Jenkins
2. Bamboo
3. Circle CI
4. Github Actions
5. Azure Devops
6. AWS CodePipeline

# Jenkins
* Jenkins is a self-contained, java-based-open source automation server which can be used to automate all sorts of tasks related to building, testing, and delivering or deploying software. 
  
## Before And After Jenkins

![preview](Images/jenkins1.jpg)

## Feature of Jenkins
 ![preview](Images/jenkins4.png)

### Installing Jenkins in EC2 Instance.
* Create an EC2 instance of Ubuntu flavour(linux OS).In security groups allow 22 and 8080.
* Jenkins runs on 8080 port.

    ![preview](Images/jenkins7.png)

* Jenkins need minimum java-17.So we have to install java-17 or above.
  
    ![preview](Images/jenkins8.png)

* [Refer Here](https://www.jenkins.io/doc/book/installing/) for installation 
* Select the required 

    ![preview](Images/jenkins5.png)
    ![preview](Images/jenkins6.png)

* After Installing Jenkins we can see jenkins page by entering `http://<publicip>:8080` in browser

    ![preview](Images/jenkins9.png)

* Next we have to go the path mentioned in the page and get the password to login.
  
    ![preview](Images/jenkins10.png)
    ![preview](Images/jenkins11.png)

* Install plugins you can select the plugins or else you can install the suggested plugins.
   
    ![preview](Images/jenkins12.png)

* Create an admin user.
  
    ![preview](Images/jenkins13.png)
    ![preview](Images/jenkins14.png)
    ![preview](Images/jenkins15.png)

* After setting up that now we can see the dashboard.  

    ![preview](Images/jenkins16.png)

### Installing Plugins
*  Going to manage jenkins -->Plugins
  
  ![preview](images/jenkins29.png)

* In plugins --> Available plugins --> search for plugin you need.Now click on install
  
  ![preview](images/jenkins30.png)

* After installing the Jenkins page will restart again, so login and see in installed plugins.
  
  ![preview](images/jenkins27.png)

* Now manage Jenkins --> system --> Declarative pipeline fill the details
 
 ![preview](images/jenkins28.png)

### Terms in Jenkins
* Job/Project: This is set of steps configured as one unit (Job/Project)
* Workspace
* Jenkins Home: This is home directory for the user jenkins which got created as part of jenkins installation.
* Default on linux /var/lib/jenkins
* Jenkins stores everything in jenkins home directory.
* If we click on  New item then we can see what are the option jenkins is providing for jobs
  
  ![preview](images/jenkins18.png)

### Jenkins – Free Style Project
* This project is created with Jenkins UI.
* Give name of the job and select freestyle project. Then click on ok.
  
  ![preview](images/jenkins19.png)
  ![preview](images/jenkins20.png)
* The Sections are
    * General: Give metadata and basic settings
    * Source Code Management: Where the SCM (git details)
    * Build Triggers: When to build
    * Build Environment: Additonal environmental steps
    * Build Steps: Actual build steps
    * Post Build Actions: After success or failure what has to be done
* Create a jenkins free style project (UI/Classic) which shows the current user and environment variables.
  
  ![preview](images/jenkins21.png)

* Select the build steps that you want to perform. For showing current user and env variable we have to select execute shell. Then give the commands and then save.
   
   ![preview](images/jenkins22.png)
   ![preview](images/jenkins23.png)
   ![preview](images/jenkins24.png)
   ![preview](images/jenkins25.png)
   ![preview](images/jenkins26.png)

* [Refer here](https://directdevops.blog/2023/11/22/devops-classroom-notes-22-nov-2023/) for reference exploring free-style project.
 
### Jenkins Distributed Architecture

* Jenkins uses a Master-Slave architecture to manage distributed builds. 
  
  ![preview](images/jenkins17.png)

#### Jenkins Master

**Your main Jenkins server is the Master. The Master’s job is to handle:**

* Scheduling build jobs.
* Dispatching builds to the slaves for the actual execution.
* Monitor the slaves (possibly taking them online and offline as required).
* Recording and presenting the build results.
* A Master instance of Jenkins can also execute build jobs directly.
  
#### Jenkins Slave

**A Slave is a Java executable that runs on a remote machine. Following are the characteristics of Jenkins Slaves:**

* It hears requests from the Jenkins Master instance.
Slaves can run on a variety of operating systems.
* The job of a Slave is to do as they are told to, which involves executing build jobs dispatched by the Master.
* You can configure a project to always run on a particular Slave machine or a particular type of Slave machine, or simply let Jenkins pick the next available Slave.

### Slave Configuration.
* Install java-17 on the node because java-17 is required for jenkins to connect as node.
* I am adding docker server as agent in Jenkins. So have to install docker  in that server.
  
  ![preview](images/jenkins31.png)
  ![preview](images/jenkins32.png)
  ![preview](images/jenkins33.png)
  ![preview](images/jenkins34.png)

* We have to select the credentials or else click on add to create one.
  
  ![preview](images/jenkins35.png)
  ![preview](images/jenkins36.png)
  ![preview](images/jenkins37.png)

* After setting up we can see the node is online.
  
  ![preview](images/jenkins38.png)

### Pipeline as code

* This approach is defining steps required for building CI/CD expressed as a code in version control system.
* Advantages:
    * Changes done in pipeline over a period of time will have history in git.
    * Per branch i can different build steps
    * It also allows to create reusability
* Jenkins started doing Pipeline as code with Scripted Pipelines and then they have also provided Declarative Pipelines
* **Scripted Pipeline:**
    * This is the Pipeline expressed in groovy language.
    * These pipelines are very much useful if your CI/CD pipeline has complex steps.
* **Declartive Pipeline:**
    * This pipeline is expressed in the form of Jenkins DSL (Domain Specific Language) which internally uses groovy.
    * This has been implemented to reduce the learning curve.
* The Pipeline as Code in Jenkins can be expressed in any file but file with name `Jenkinsfile` is commonly used 
* Jenkinsfile is nothing but writing a declarative pipeline and store it in github where we can get from there and run the pipeline.

#### Declarative Pipeline
* [Pipeline syntax](https://www.jenkins.io/doc/book/pipeline/syntax/) to write a declarative pipeline.
  
  ![preview](images/jenkins46.webp)
* Click on new item --> Name --> select pipeline --> ok
  
 ![preview](images/jenkins39.png)

* In general we are using github project we have to mention the url.
  
 ![preview](images/jenkins40.png)

* In build trigger we can mention when the pipeline have to run.
 
 ![preview](images/jenkins41.png)
 
* In advanced project options we have two options   
    1. pipeline script
    2. pipeline script from SCM

 ![preview](images/jenkins42.png)

* First we will try pipeline script
  
  ![preview](images/jenkins43.png)

* If we click on pipeline syntax.
* Snippet Generator will provide the code that you select. For example I selected the git then it will provide the syntax
  
  ![preview](images/jenkins44.png)
  ![preview](images/jenkins45.png)
  
* We can copy and use in pipeline.
  
```Jenkinsfile
pipeline {

    agent any

    triggers {

        pollSCM('* * * * *')

    }

    stages {
        stage('checkout') {
            steps {
                git url: 'https://github.com/tejaswini1811/Nodejs_project.git',
                    branch: 'test'
            }
        }

        // Building Docker image
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build "hello:1" // I am using docker plugin
                }
            }
        }
    }
}
```

![preview](images/jenkins46.png)

* Now build the pipeline and wait for the pipeline to run.

  ![preview](images/jenkins47.png)
  ![preview](images/jenkins48.png) 
  ![preview](images/jenkins49.png)

*  We can see the details of our jenkins in server level in /var/lib/jenkins
  ![preview](images/jenkins50.png)
 
* In workspace details of our jobs will be present.
* In above pipeline I have used docker plugin, without docker plugin we have to give the command directly.
```Jenkinsfile
pipeline {

    agent any

    triggers {

        pollSCM('* * * * *')

    }

    stages {
        stage('checkout') {
            steps {
                git url: 'https://github.com/tejaswini1811/Nodejs_project.git',
                    branch: 'test'
            }
        }

        // Building Docker image
        stage('Building image') {
            steps{
                 
                sh 'docker image build -t hello:2 .'
            }
        }
    }
}
```
* After build 

  ![preview](images/jenkins51.png)