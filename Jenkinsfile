pipeline {
    agent any

    tools {
         maven 'maven-3.9.0'
    }

    stages {
        stage ("Lint Checks") {
            steps {
                sh "echo starting lintChecks"
                sh "mvn checkstyle:check || true"
                sh "echo LintChecks completed"
            }
        }
    }
}