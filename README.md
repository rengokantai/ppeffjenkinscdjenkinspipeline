# ppeffjenkinscdjenkinspipeline
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
