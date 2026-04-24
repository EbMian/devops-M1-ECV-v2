pipeline {
    agent any 
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
            stage("Build") {
                steps {
                    sh 'docker ../build'
                }
            }
                
        }

    
}