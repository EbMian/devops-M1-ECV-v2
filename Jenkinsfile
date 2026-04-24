pipeline {
    agent any 

        options {
            disableConcurrentBuilds() // interdit le fait de lancer ce job 2 fois en meme temps
            parallelsAlwaysFailFast() // dans un parallel, si l'un des threads échoue, on stoppe les autres
        }

        environment {
            IMAGE_NAME = "task-api"
        }

        stages {
            stage("Install")
            {
                steps {
                    sh 'npm ci'
                }
                
            }
            // Lancez les tests et le lint
            stage("Qualité") {
                parallel {
                    stage("Lint")
                    {
                        steps {
                            sh 'npm run lint'
                        }
                    }
                    stage("Tests")
                    {
                        steps {
                            sh 'npm run test:coverage'
                        }
                    }
                }
            }
            // Build docker de cette image en utilisant le daemon de l'hote
            stage('Compose Build/Up') {
                steps {
                    sh '''
                    docker build ${IMAGE_NAME}:${BUILD_NUMBER} .
                    docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${IMAGE_NAME}:latest
                    '''
                }
            }
            

            stage("Deploy") {
                steps {
                    sh 'docker run -d -p $IMAGE_NAME}:${BUILD_NUMBER}'
                }
            }


            stage("Test") {
                steps {
                    sh 'curl host.internal.docker:3000/health'
                }
            }
        }

    
}