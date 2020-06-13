pipeline {
	environment{
		registro="redinskala/rsphp"
		registroID="redin_DockerHub"
		dockerImage=""
		dockerImageLatest=""
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
				script{
					dockerImage=docker.build registro + ":$BUILD_NUMBER"
					dockerImageLatest=docker.build registro + ":latest"
				}
				sh 'docker images'
			}
		}
		stage('Push a DockerHub'){
			steps{
				script{
					docker.withRegistry('',registroID){
						dockerImage.push()
					}
					docker.withRegistry('',registroID){
						dockerImageLatest.push()
					}
				sh 'docker image rm $registro:$BUILD_NUMBER $registro:latest'
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
