pipeline{
    agent any
    stages{
        //primera etapa pa parar todos los servicios
        stage('Deteniendo los servicios'){
            steps{
                sh '''
                    docker compose -p adj-demo-c down || true
                '''
            }
        }
        //eliminar
        stage('Eliminando Imagenes antañas'){
            steps{
                sh '''
                    IMAGES=$(docker images --filter "label=com.docker.compose.project=adj-demo-c" -q)
                    if[-n '$IMAGES']; then
                    docker images rmi $IMAGES
                else
                    echo 'no hay imagenes pa borrar'
                fi
                '''
            }
        }
        //bajar actualizacion
        stage('Actuyalizando...'){
            steps{
                checkout scm
            }
        //levantar y desplegar
        stage('Construyendo y desplegando...'){
            steps{
                sh '''
                    docker compose up --build -d
                '''
            }
        }
    }

    post{
        success{
            echo 'Pipeline ejecutado bien'
        }

        failure{
            echo 'error al ejecutar al Pipeline'
        }

        always{
            echo 'Pipeline finalizado'
        }
    }
}