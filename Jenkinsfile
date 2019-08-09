Jenkinsfile (Declarative Pipeline)
pipeline {
    agent { 
        docker { image 'python:3.5.1' } 
    }
    stages {
        stage('build') {
            steps {
                sh 'python --version'
                sh 'echo "Hello World"'
            }

            timeout(time: 3, unit: 'MINUTES') { //nested retry with timeout
                retry (5) {
                    sh 'echo "Timeout Test"'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
            }
        }
        stage('Sanity check') {
            steps {
                input "Does the staging environment look ok?"
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}