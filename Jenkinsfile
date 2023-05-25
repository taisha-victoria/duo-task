pipeline {
	// blah
	agent any
	stages {
		stage('pre-build clean') {
			steps {
				sh 'docker system prune -f'
			}
		}
		stage('build containers') {
			steps {
				sh '''
				docker network create duo-net
				docker build -t duo-app:v1 .
				docker run -d --network duotask-net --name flask-app duo-app:v1
				docker run -d --network duotask-net --name nginx --mount type=bind,source=$(pwd)/nginx.conf,target=/etc/nginx/nginx.conf -p 80:80 nginx:alpine
				'''
			}
		}
	}
