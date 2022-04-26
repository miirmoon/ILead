pipeline {
	agent any

	tools {
		nodejs "nodejs-ilead"
	}

  stages {
    stage('jenkins test') {
      steps {
        echo 'Hello Jenkins!'
      }
    }
    stage('React install') {
      steps {
        sh 'npm i ./FE/ilead -g'
      }
    }
    stage('React build') {
      steps {
        sh 'npm run build --prefix FE/ibg'
      }
    }
    stage('Build nginx image') {
      steps {
        sh 'docker build -t basepage/nginx ./FE/ilead'
      }
    }
    stage('React Deploy') {
			steps{
				sh 'docker stop nginx && docker rm nginx'
				sh 'docker run --network ilead -d --name nginx -p 80:80 -p 443:443 -v /etc/letsencrypt:/etc/letsencrypt -u root basepage/nginx'
			}
		}
  }
}