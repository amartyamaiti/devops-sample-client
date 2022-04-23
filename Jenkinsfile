pipeline{
    agent any
    stages{
        stage("Build"){
            steps{
                sh "npm install"
                sh "npm run build"
            }
        }
        stage("Unit test"){
            steps{
                sh "echo 'Todo unit test'"
                //sh "npm run test"
            }
        }
        stage("Verify tools"){
            steps{
                sh '''
                docker version
                docker compose version
                '''
            }
        }
        stage("Image build"){
            steps{
                //remove old image
                sh "docker image rm devops-client-image"
                sh "docker build -t devops-client-image"
            }
        }
        stage("Remove old container"){
            steps{
                sh 'docker compose down --rmi local --volumes'
            }
        }
        stage("Start container"){
            steps{
                sh 'docker compose up -d --wait'
                sh 'docker compose ps'
            }
        }
        stage("SonarQube analysis"){
            steps{
                script{
                    def scannerHome= tool 'SonarQubeScan';
                    withSonarQubeEnv('Sonarqube'){
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=devops-client -Dsonar.projectName=devops-client"
                    }
                }
            }
        }
    }
}