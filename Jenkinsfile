pipeline {
      
    agent any
   
    stages {
        
        stage('Set ENV for branch') {
            steps {
                script {
                    def commit = checkout scm
                    // we set BRANCH_NAME to make when { branch } syntax work without multibranch job
                    env.BRANCH_NAME = commit.GIT_BRANCH.replace('origin/', '')
                    echo "${env.BRANCH_NAME}"
                }
            }
        }

        
        stage ('Checkout') {
            
            when {
                anyOf{
                    expression { env.BRANCH_NAME == "develop" }
                    expression { env.BRANCH_NAME == "main" }
                    expression { env.BRANCH_NAME ==~ "release/*" }
                         
                }
            }
    
        

            steps {
                
                echo "Test stage1 run successfully..! " 
                //checkout scmGit(branches: [[name: '*/main'], [name: '*/develop'], [name: '*/release/*']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHub-rootuser', url: 'https://github.com/sohailsayyed/jenkins_test.git']])

                echo "${env.BRANCH_NAME}"

                //sh 'npm install'
                //sh 'nohup node server.js &'
            }
            
        }

        stage('Final Steps') {

             when {
                anyOf{
                    expression { env.BRANCH_NAME == "main" }
                    expression { env.BRANCH_NAME ==~ "release/*" }
                }
            }

            steps {

                sh 'pwd'
		
                //sh 'aws s3 sync . s3://cloudtrail-test-12345/'
                //sh 'pwd'
                //sh 'scp -rv *  ubuntu@13.233.236.84:/home/ubuntu/jenkins_test/'
                //sh 'node app.js'
                
                echo "+++Upload Successful+++"
            }
        }
  
    }
}
