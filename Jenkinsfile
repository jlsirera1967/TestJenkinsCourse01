pipeline 
{
    agent any
    stages {
        stage('Generate Value') {
            steps {
                script {
                    // Generamos un valor dinámico (ejemplo: timestamp)
                    env.BUILD_TAG_CUSTOM = "build-${new Date().format('yyyyMMddHHmmss')}"
                    echo "Valor generado: ${env.BUILD_TAG_CUSTOM}"
                    env.VERSION = "1.0.${env.BUILD_NUMBER}"
                }
            }
        }

        stage('Use Value') {
            steps {
                script {
                    // Reutilizamos la variable generada en la stage anterior
                    echo "Reutilizando el valor en otra stage: ${env.BUILD_TAG_CUSTOM}"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Desplegando usando el tag: ${env.BUILD_TAG_CUSTOM}"
                    echo "Versión tag: ${env.VERSION}"
                    ls -l
                }
            }
        }
    }
}
