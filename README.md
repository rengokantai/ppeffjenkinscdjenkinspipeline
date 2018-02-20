# ppeffjenkinscdjenkinspipeline

### Intro
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
      }
    }
  }
}
```
