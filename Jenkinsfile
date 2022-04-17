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
                sh "npm run test"
            }
        }
    }
}