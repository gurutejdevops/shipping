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
        stage("Quality Gate") {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage ("Generating Artifact") {
            steps {
                sh "echo generating Artifact"
                sh "mvn clean package"
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