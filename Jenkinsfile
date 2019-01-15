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

    }
}
