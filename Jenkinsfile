pipeline{

    agent any

    stages{

        stage('sonar qulity check'){
            agent{

                docker{
                    image 'maven'
                }
            }
            steps{

                scripts{
                   withSonarQubeEnv(credentialsId: 'sonar-token') {
                    sh 'sonar-scanner'
                   } 
                }

            }
        }
    }

}