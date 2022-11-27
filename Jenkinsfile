pipeline {
    agent any
    stages {
        stage('Pull Source Code') {
            steps {
                git branch: "main", url: 'https://github.com/calmond1/DevOpsDemo/'
            }
        }
        stage('Prune Docker Data'){
            steps {
                sh '/usr/bin/docker system prune -a -f'   
            }
        }
        stage('Test The Build'){
			steps{
				sh '/usr/bin/docker build -t devopsdemotest -f ./Dockerfile.test .'
			}
        }
        stage('Docker Compose Build'){
			steps{
				sh 'DOCKER_BUILDKIT=0 /usr/local/bin/docker-compose build'
			}
        }
        stage('Docker Compose Up'){
			steps{
				sh '/usr/local/bin/docker-compose down'
				sh '/usr/local/bin/docker-compose up -d'
			}
        }
    }
}
