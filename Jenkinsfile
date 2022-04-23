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
                //sh "npm run test"
            }
        }
        stage("verify tools"){
            steps{
                sh '''
                docker version
                docker compose version
                '''
            }
        }
        stage("Remove old docker data"){
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
        stage("SonarQube analysis devops-client"){
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