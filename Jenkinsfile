pipeline {
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
				sh 'docker images'
			}
		}
		stage('Servicio rsphp+rsmysql'){
			steps{
				sh 'docker-compose up -d'
				sh 'docker-compose down'
			}
		}
	}
}
