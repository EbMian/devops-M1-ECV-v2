pipleline {
    agent any {
        stages {
            stage ("install")
            {
                steps {
                    sh 'npm ci'
                }
                
            }
            // Lancezz les tests et le lint
            stage("lint")
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