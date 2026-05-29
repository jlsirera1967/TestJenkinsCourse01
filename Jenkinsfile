pipeline {
    agent any
    options {
        ansiColor('xterm') // Habilita colores ANSI
        timestamps()       // Opcional: añade timestamps a logs
    }
    stages {
        stage('Preparación') {
            steps {
                script {
                    echo "\u001B[34m[PREPARACIÓN] Iniciando preparación del entorno...\u001B[0m"
                }
                sh 'ls -la'
            }
        }
        stage('Procesamiento en paralelo') {
            parallel {
                stage('datos1.txt') {
                    steps {
                        script {
                            def prefix = "\u001B[32m[datos1]\u001B[0m"
                            echo "${prefix} Procesando datos1.txt"
                            sh "cat datos1.txt"
                            echo "${prefix} Simulando procesamiento pesado..."
                            sleep 5
                            echo "${prefix} Procesamiento finalizado"
                        }
                    }
                }
                stage('Datos2.txt') {
                    steps {
                        script {
                            def prefix = "\u001B[33m[Datos2]\u001B[0m"
                            echo "${prefix} Procesando Datos2.txt"
                            sh "cat Datos2.txt"
                            echo "${prefix} Simulando procesamiento pesado..."
                            sleep 5
                            echo "${prefix} Procesamiento finalizado"
                        }
                    }
                }
                stage('datos3.txt') {
                    steps {
                        script {
                            def prefix = "\u001B[36m[datos3]\u001B[0m"
                            echo "${prefix} Procesando datos3.txt"
                            sh "cat datos3.txt"
                            echo "${prefix} Simulando procesamiento pesado..."
                            sleep 5
                            echo "${prefix} Procesamiento finalizado"
                        }
                    }
                }
                stage('Rama con error') {
                    steps {
                        script {
                            def prefix = "\u001B[31m[ERROR]\u001B[0m"
                            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                                // catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE')
                                echo "${prefix} Esta rama fallará intencionadamente"
                                sleep 2
                                // Error real
                                error("${prefix} Fallo intencional en procesamiento")
                            }
                
                            echo "${prefix} El error ha sido capturado, el pipeline continúa"
                        }
                    }
                }
            }
        }
        stage('Resumen') {
            steps {
                script {
                    echo "\u001B[35m[RESUMEN] Todos los procesos en paralelo han terminado (algunos pueden haber fallado).\u001B[0m"
                }
            }
        }
    }
    post {
        failure {
            echo "\u001B[31m[POST] El pipeline ha fallado debido a errores en alguna rama.\u001B[0m"
        }
        success {
            echo "\u001B[32m[POST] Pipeline completado correctamente.\u001B[0m"
        }
        always {
            echo "\u001B[36m[POST] Ejecución finalizada.\u001B[0m"
        }
    }
}

