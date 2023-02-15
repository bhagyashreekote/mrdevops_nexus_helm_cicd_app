pipeline{

    agent any

    stages{

        stage('soanr qulity check')
            agent{

                docker{
                    image 'maven'
                }
            }
            steps{
                scripts{
                   withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'mvn clean package sonar:sonar'
                    } 
                }

            }

    }




}