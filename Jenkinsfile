pipeline {
    agent any
    stages {
        stage ('Build Servlet Project') {
            steps {
                /*For Mac & Linux machine */
                sh 'mvn clean install'
            }

            post{
                success{
                    echo 'Now Archiving ....'
                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }

        stage ('Deploy Build in Staging Area') {
            steps{
                build job : 'Deploy-Staging-Area-Pipeline'
            }
        }

        stage ('Deploy to production') {
            steps{
                timeout (time: 5, unit: 'Day') {
                    input message: 'Approve PRODUCTION Deployment?'
                }

                build job : 'Deploy-Production-Pipeline'
            }

            post{
                success{
                    echo 'Deployment on Production is Successful'
                }

                failure{
                    echo 'Deployment Failure on Production'
                }
            }
        }
    }
}
