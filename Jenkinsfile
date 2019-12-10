pipeline {
	environment{
		registro="redinskala/rsphp"
		registroID="redin_DockerHub"
		dockerImage=""
	}
        agent any
        stages{
                stage('Paso 1'){
                        steps{
                                sh 'echo Paso 1'
                        }
                }
		stage('Verificando Docker'){
			steps{
				sh 'docker images'
			}
		}
		stage('Construir rsphp'){
			steps{
				sh 'docker-compose down'
				sh 'docker image rm rsphp'
				sh 'docker build --tag=rsphp .'
				dockerImage=docker.build registry + ":dev"
				sh 'docker images'
			}
		}
		stage('Push a DockerHub'){
			steps{
				docker.withRegistry('',registroID){
					dockerImage.push()
				}
			}
		}
		stage('Servicio rsphp+rsmysql'){
			steps{
				sh 'docker-compose up -d'
			}
		}
	}
}
