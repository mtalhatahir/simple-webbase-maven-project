pipeline{
    agent any
    tools {
        maven 'mavenjenkins'
    }
    stages{
        stage('git-pull'){
            steps{
                git credentialsId: 'GitHubCreds', url: 'https://github.com/mtalhatahir/simple-webbase-maven-project.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Deploy'){
            steps{
                sshagent(['admin1']) {
                    sh 'scp target/vertx-start-project-1.0-SNAPSHOT-fat.jar admin1@192.168.117.128:Deployments/Maven/'
                }
            }
        }
        stage('run-app'){
            steps{
                sshagent(['admin1']) {
                    sh '''ssh -tt -o StrictHostKeyChecking=no admin1@192.168.117.128 "cd Deployments/Maven/; java -jar vertx-start-project-1.0-SNAPSHOT-fat.jar" '''
                }
            }
        }
    }
}