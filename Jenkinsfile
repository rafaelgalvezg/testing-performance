pipeline {
    agent {
        docker {
            image 'alpine/jmeter:5.6.3'
            args '--entrypoint=""'
        }
    }
    stages {
        stage('Performance Tests') {
            steps {
                node { // Agregar el bloque node
                    sh 'jmeter -n -t PetClinic.jmx -l petclinic-results.jtl'
                }
            }
        }
        stage('Publish Results') {
            steps {
                node { // Agregar el bloque node
                    perfReport sourceDataFiles : 'petclinic-results.jtl'
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
