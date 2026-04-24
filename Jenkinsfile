pipleline {
    agent any {
        stages {
            stage ("Install")
            {
                steps {
                    sh 'npm ci'
                }
                
            }
            // Lancezz les tests et le lint
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
                            sh 'npm run tests:coverage'
                        }
                    }
                }
            }
            
                
        }
    }
    
}