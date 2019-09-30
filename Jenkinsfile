pipeline {
    agent { docker 'python:3.5.1' }

    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'mysql'
    }

    stages {
        stage('build') {
            steps {
                sh 'python --version'
                echo "hello world!"
		echo $DB_ENGINE
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
