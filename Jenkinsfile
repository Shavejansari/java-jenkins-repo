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
                script {
                    def maven_exists = fileExists('/usr/share/maven')
                    if (maven_exists == true) {
                        echo 'Skipping Maven install - already exists'
                    } else {
                        sh 'sudo apt-get update -y && sudo apt-get upgrade -y'
                        sh 'sudo apt install -y wget tree unzip openjdk-11-jdk maven'
                    }
                }
            }
        }
        stage('Download Java Code') {
            steps {
                git branch: 'main', credentialsId: 'git-repo-creds', url: 'git@github.com:Shavejansari/java-jenkins-repo.git'
            }
        }
        stage('Compiling and Running Test Cases') {
            steps {
                sh 'mvn clean'
                sh 'mvn compile'
                sh 'mvn test'
            }
        }
        stage('Creating Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Deploying Application') {
            steps {
                script {
                    withEnv(['JENKINS_NODE_COOKIE=dontkill']) {
                        sh """
                            nohup java -jar ./target/jenkin-java-training-0.0.1-SNAPSHOT.jar &
                        """
                    }
                }
            }
        }
    }
}
