pipeline {
    agent any

    environment {
        MAVEN_HOME = "${env.MAVEN_HOME}"  // Use the system environment variable
        PATH = "${MAVEN_HOME}\\bin;${env.PATH}"  // Add Maven to PATH
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/IvanGutierrrez/PracticeCalidad.git'

                // Run Maven on a Unix agent.
                bat "mvn clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}