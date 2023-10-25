pipeline {
    agent any
    stages {
        stage('Delete the workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Second Stage') {
            stages {
                echo "Second stage"
            }
        }
        stage('Third Stage') {
            steps {
                echo "Third stage"
            }
        }
    }
}
