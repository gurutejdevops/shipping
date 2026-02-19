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
        stage ("Code Compile") {
            steps {
                sh "echo Code compile"
                sh "mvn clean compile"
            }
        }
        // stage ("SonarQUbe Scan") {
        //     steps {
        //         sh "echo sonarqube scanning started"
        //         // withSonarQubeEnv('SonarQube-Server') {
        //         //     sh '''
        //         //         mvn sonar:sonar \
        //         //         -Dsonar.projectKey=shipping \
        //         //         -Dsonar.projectName=shipping
        //         //     '''
        //         // }
        //     }
        // }
        // stage("Quality Gate") {
        //     steps {
        //         timeout(time: 5, unit: 'MINUTES') {
        //             waitForQualityGate abortPipeline: true
        //         }
        //     }
        // }

        stage("Unit Test") {
            steps {
                sh "echo unit tests"
                sh "mvn test"
            }
        }
        stage ("Generating Artifact") {
            when {
                expression { env.TAG_NAME != null }
            }
            steps {
                sh "echo generating Artifact"
                sh "mvn clean package"
                
            }
        }
        stage ("Uploading Artifact") {
            when {
                expression { env.TAG_NAME != null }
            }
            steps {
                sh "echo uploading Artifact"
            }
        }

    }
}

// stage("Quality Gate") {
//     steps {
//         script {
//             timeout(time: 2, unit: 'MINUTES') {
//                 def qg = waitForQualityGate()
//                 echo "Quality Gate Status: ${qg.status}"
//                 if (qg.status != 'OK') {
//                     error "Quality Gate Failed!"
//                 }
//             }
//         }
//     }
// }