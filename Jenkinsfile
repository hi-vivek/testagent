pipeline {
    agent any
    options {
            buildDiscarder(logRotator(numToKeepStr: "5"))
            }
    stages {
            
        stage('see var') {
                steps {
                       sh '''
                         echo "hello"
                         echo $GIT_BRANCH
                        '''              
            }
        }


            stage('Dev Deployment') {
                agent {
                    label 'dev'
                }
                when {
                    expression { GIT_BRANCH ==~ /origin\/(dev|develop)/ }
                }
                steps {
                       sh '''
                         echo "hello dev"
                         pwd
                         ls /home/ec2-user
                        '''                   
                
            }
        }
        
            stage('QA Deployment') {
                when {
                    expression { env.GIT_BRANCH ==~ /origin\/qa/) }
                }
                steps {
                       sh '''
                         echo "hello qa"
                         pwd
                         ls /home/ec2-user
                        '''                    
            }
        }
    }
}
