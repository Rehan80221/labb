pipeline {
    agent any
    environment {
        REPO_URL = 'https://github.com/Rehan80221/labb.git'  // Replace with your Git repository URL
        BUILD_TOOL = 'mvn'                            // Use 'gradle' if required
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: "${REPO_URL}" // Adjust branch as needed
            }
        }
        stage('Build Project') {
            steps {
                script {
                    if (env.BUILD_TOOL == 'mvn') {
                        sh 'mvn clean package'
                    } else if (env.BUILD_TOOL == 'gradle') {
                        sh './gradlew build'
                    }
                }
            }
        }
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true // Adjust for Gradle if needed
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
