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

        stage('create AWS ec2 instance') {
            steps {
                withAWS(credentials: 'jenkins_aws', region: 'us-east-1') {
                    sh "aws ec2 run-instances --image-id ami-0c2b8ca1dad447f8a --count 1 --instance-type t2.micro --key-name june2021 --security-group-ids sg-0be7cfd24c5af82b6 --subnet-id subnet-6e081250"
                }
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
