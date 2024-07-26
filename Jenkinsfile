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
                sh 'jmeter -n -t PetClinic.jmx -l petclinic-results.jtl'
            }
        }
        stage('Publish Results') {
            steps {
                perfReport sourceDataFiles : 'petclinic-results.jtl'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
