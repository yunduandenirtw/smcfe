pipeline {
 
 agent any
 
  stages {
    stage('Build') {
    
      steps {
        echo 'start npm install...'
        bat 'npm install'
        echo 'start npm build...'
        bat 'npm run build'
        echo 'npm install and build successfully!'
      }
    }

    stage('docker build & push & run') {
    
      steps {
       
        withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          echo '%USERNAME%'
          echo '%PASSWORD%'
          bat 'docker login -u %USERNAME% -p %PASSWORD%'
          bat 'docker image build -t yunduandenirtw/smcfe .'
          bat 'docker push yunduandenirtw/smcfe'
          bat 'docker run -d -p 4200:80 --name smcfe yunduandenirtw/smcfe'
        }  
      }
    }

  }
}


