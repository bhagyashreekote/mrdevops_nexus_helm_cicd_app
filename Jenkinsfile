pipeline{

    agent any
    environment {

        VERSION = "${env.BUILD_ID}"
    }

    stages{

        stage('GIT checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/sagarkulkarni1989/mrdevops_nexus_helm_cicd_app.git'
            }
        }
        // stage('UNIT Test'){
            
        //     steps{
        //         sh 'mvn test'
        //     }
        // }
        // stage('Integration Test'){
            
        //     steps{
        //         sh 'mvn verify -DskipUnitTests'
        //     }
        // }
        // stage('Maven Build'){
            
        //     steps{
        //         sh 'mvn clean install'
        //     }
        // }
        stage('Static code Analysis'){

            agent{

                docker {
                    image 'maven'

                }

            }
            
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token'){
                     sh 'mvn clean package sonar:sonar'   
                    }
                }
                
   
            }
                
            
        }
        stage('Quality gate'){
            
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                     
                    
                }
                
   
            }
                
            
        }
        stage('docker build & docker push to Nexus repo'){

            steps{

                script{
                    withCredentials([string(credentialsId: 'nexus_passwd', variable: 'nexus_creds')]) {
                         sh '''
                            docker build -t 3.111.38.46:8083/springapp:${VERSION} . 

                            docker login -u admin -p $nexus_creds 3.111.38.46:8083 

                            docker push 3.111.38.46:8083/springapp:${VERSION}

                            docker rmi 3.111.38.46:8083/springapp:${VERSION}

                         '''



                    }


                }
            }

           


        }
        stage('Identiying misconfigs using datree in helm charts'){

            steps{

                script{

                    dir('kubernetes/myapp/') {

                        sh 'helm datree test .'
                        
                    }

                }

            }
        }
       
    }

}