pipeline{

    agent any
    // environment {

    //     VERSION = "${env.BUILD_ID}"
    // }

    stages{

        stage('GIT checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/sagarkulkarni1989/mrdevops_nexus_helm_cicd_app.git'
            }
        }
         stage('Code Compile') {
            steps {
                sh "mvn clean compile"
            }
        }
        stage('Unit test and jacoco') {
            steps {
                sh "mvn test"
            }
            post {
              always {
                    junit 'target/surefire-reports/*.xml'
                    jacoco execPattern: 'target/jacoco.exec'
              }
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
        // stage('Static code Analysis'){

        //     agent{

        //         docker {
        //             image 'maven'

        //         }

        //     }
            
        //     steps{
        //         script{
        //             withSonarQubeEnv(credentialsId: 'sonar-token'){
        //              sh 'mvn clean package sonar:sonar'   
        //             }
        //         }
                
   
        //     }
                
            
        // }
        // stage('Quality gate'){
            
        //     steps{
        //         script{
        //             waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                     
                    
        //         }
                
   
        //     }
                
            
        // }
           stage('Static code analysis'){
            
                steps{
                
                     script{
                    
                        withSonarQubeEnv(credentialsId: 'sonar-token') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
            }
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                    }
                }
            } 











        // stage('docker build & docker push to Nexus repo'){

        //     steps{

        //         script{
        //             withCredentials([string(credentialsId: 'nexus_passwd', variable: 'nexus_creds')]) {
        //                  sh '''
        //                     docker build -t 3.108.55.62:8083/springapp:${VERSION} . 

        //                     docker login -u admin -p $nexus_creds 3.108.55.62:8083 

        //                     docker push 3.108.55.62:8083/springapp:${VERSION}

        //                     docker rmi 3.108.55.62:8083/springapp:${VERSION}

        //                  '''



        //             }


        //         }
        //     }

           


        // }
        // stage('Identiying misconfigs using datree in helm charts'){

        //     steps{

        //         script{

        //             dir('kubernetes/myapp/') {

        //                 withEnv(['DATREE_TOKEN=2758595d-63ec-4966-b884-905cbd48647a']){
        //                 sh 'helm datree test .'

        //                 }

                        
                        
        //             }

        //         }

        //     }
        // }

        //    stage(' Pushing the helm chart to nexus repo'){

        //         steps{

        //             script{

        //                      withCredentials([string(credentialsId: 'nexus_passwd', variable: 'nexus_creds')]) {

        //                          dir('kubernetes/myapp/') {

        //                              sh '''

        //                              helmversion=${helm show chart myapp | grep version | cut -d: -f 2 | tr -d ' ' }
        //                              tar -czvf myapp-${helmversion}.tgz myapp/
        //                              curl -u admin:$nexus_creds http://3.108.55.62:8081/repository/helm-repo/ --upload-file myapp-${helmversion}.tgz -v

        //                             '''

        //                         }

        //                     }

                  

        //             }
        //         }


        //    }
       
    }

}
