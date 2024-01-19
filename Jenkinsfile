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
                when {
                    expression { GIT_BRANCH ==~ /origin\/(dev|develop)/ }
                }
                steps {
                      withCredentials([string(credentialsId: 'dev-db-password', variable: 'QA_V2_WAKA_DATABASE_PASSWORD')])
                       {
                       sh '''
                         echo "hello dev"
                        '''
                    }                    
                
            }
        }
        
            stage('QA Deployment') {
                when {
                    expression { env.GIT_BRANCH ==~ /origin\/qa/) }
                }
                steps {
                       withCredentials([usernamePassword(credentialsId: 'nexus_credential', passwordVariable: 'NEXUS_PASSWORD', usernameVariable: 'NEXUS_USER'), string(credentialsId: 'qa-db-password', variable: 'QA_V2_WAKA_DATABASE_PASSWORD')])
                       {
                       sh '''
                         echo "hello qa"
                        '''
                    }                    
            }
        }
    }
}
