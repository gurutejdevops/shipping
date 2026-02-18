pipeline {
    agent any

    tools {
         maven 'maven-3.9.0'
        //  sonarScanner 'sonarscanner-4.5.0.2216'
    }

    stages {
        stage ("Lint Checks") {
            steps {
                sh "echo starting lintChecks"
                sh "mvn checkstyle:check || true"
                sh "echo LintChecks completed"
            }
        }

        stage ("Generating Artifact") {
            steps {
                sh "echo generating Artifact"
                sh "mvn clean package"
            }
        }

        stage ("SonarQUbe Scan") {
            steps {
                withSonarQubeEnv('SonarQube-Server') {
                    sh '''
                        mvn sonar:sonar \
                        -Dsonar.projectKey=shipping \
                        -Dsonar.projectName=shipping
                    '''
                }
            }
        }
    }
}