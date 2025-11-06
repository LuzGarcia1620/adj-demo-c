pipeline {
    agent any

    stages {
        // Etapa para parar tdos los servicios
        stage('Parando los servicios') {
            steps {
                script {
                    echo 'Deteniendo contenedores (Windows)...'
                    // En Windows con shell cmd, usar || exit 0 para evitar fallo si no hay contenedores
                    bat 'docker compose -p jcgr-demo down || exit 0'
                }
            }
        }

        // Elimianr las imagenes anteriores  
        stage('Borrando imagenes antiguas') {
            steps {
                script {
                    echo 'Eliminando imagenes antiguas...'
                    bat 'IMAGES=$(docker images -q jcgr-demo) && if not "%IMAGES%"=="" (docker rmi -f %IMAGES%)'
                }
            }
        }

        // Bajar la ctualizacion mas reciente
        stage('Actualizando..') {
            steps {
                checkout scm
            }
        }

        //Levantar y despegar el proyecto
        stage('Levantando los servicios') {
            steps {
                script {
                    echo 'Levantando contenedores...'
                    bat 'docker compose -p jcgr-demo up -d --build'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finalizado.'
        }
        success {
            echo 'Pipeline ejecutado exitosamente.'
        }
        failure {
            echo 'Error al ejecutar el pipeline.'
        }
    }
}