pipeline {
    agent any

    stages {
        stage('Clone Website') {
            steps {
                git url:'https://github.com/Aryanhac/Capstone-Project'
            }
        }

       stage("Docker Build Image"){
           steps{
             script{
                dockerImage = docker.build("$BUILD_NUMBER",".")
             }
           }
      }

       stage('Test Website') {
            steps {
                // Run tests on the website
                sh 'echo "Running tests on the website"'
                script {
                    branchName = sh(label: 'getBranchName', returnStdout: true, script: 'git rev-parse --abbrev-ref HEAD').trim()
                   println branchName
                }   
               
            }
       }

        stage('Push to Production') {
    
               when {
                 expression {
                    return env.BRANCH_NAME != 'master';
                }
             }
            
            steps {
                // Deploy the website to production
                sh 'echo "Deploying the website to production"'
            }
        }

    }
}


