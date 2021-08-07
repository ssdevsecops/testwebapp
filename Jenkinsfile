pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3.8"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/ssdevsecops/testwebapp.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }

        stage('sonar') {
            steps {
                sh "echo running Sonar scans"
            }
        }

        stage('veracode scan') {
             when {
                             branch 'production'
                    }
                    steps {
                        sh "echo running Sonar scans"
                    }
          }
    }
}
