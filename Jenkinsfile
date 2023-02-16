pipeline{

    agent any

    stages{

        stage('GIT checkout'){

            steps{
                git branch: 'main', url: 'https://github.com/sagarkulkarni1989/mrdevops_nexus_helm_cicd_app.git'
            }
        }
        stage('UNIT Test'){
            
            steps{
                sh 'mvn test'
            }
        }
        stage('Integration Test'){
            
            steps{
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage('Maven Build'){
            
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Static code Analysis'){
            
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token'){
                     sh 'mvn clean package sonar:sonar'   
                    }
                }
                
   
            }
                
            
        }
       
    }

}