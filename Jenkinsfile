pipeline {
    agent any
    stages {
        stage('Delete the workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Installing Java and Maven') {
            steps {
                def maven_exists = fileExists '/usr/share/maven'
                if (maven_exists == true){
                    echo 'Skipping mavn install - already exists'
                }
                else {
                    sh 'sudo apt-get update -y && sudo apt-get upgrade -y'
                    sh 'sudo apt install -y wget tree unzip openjdk-11-jdk maven'
            }
        }
        stage('Third Stage') {
            steps {
                echo "Third stage"
            }
        }
    }
}
