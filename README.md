# ppeffjenkinscdjenkinspipeline

## 2. Getting Started with Jenkins Pipeline
### My First Pipeline
(done)
### Scripted Pipeline Steps
```
node {
  stage('list directory'){
    if(isUnix()) {
      sh "ls -la"
    } else {
      bat 'dir'
    }
  }
}
```



## 4. Building with Docker

### Introduction to Docker
Note
- Docker is a software technology providing containers
- Docker provides an additional layer of abstraction and automation of operating
system-level virtualization on Windows and Linux
### Installing Docker on the Jenkins Node Server
```
groupadd docker
usermod -aG docker jenkins
```
## 5. Creating a CD pipeline
### Intro
Jenkinsfile
```
pipeline {
  agent { docker 'maven:3.5-alpine' }
  stages {
    stage ('Checkout') {
      steps {
        git 'https://'
      }
    }
    state('Build'){
      steps{
        sh 'mvn clean package'
        junit '**/target/surefire-report/TEST-*.xml'
        archiveArtifacts artifacts: 'target/*.jar', fingerprint:true
      }
    }
  }
}
```

in Jenkins:
pipeline->pipeline script from SCM

### Archiving Artefacts and Fingerprints
### Deploying Our Java
Add Deploy stage:
```
stage('Deploy'){
  steps {
    input 'Do you'
    sh 'scp target/*.jar root@host:/tar/get/'
    sh "ssh root@host 'nohup java -jar /tar/get/target.jar &'"
   }
}
```
