pipeline {
    agent any

    triggers {
        cron('H/3 * * * 1') // Runs every 3 minutes on Mondays
    }

    tools {
        maven 'Maven' // Make sure Jenkins has Maven installed and configured
        jdk 'JDK17'   // Ensure JDK is set up in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR_GITHUB_USERNAME/spring-petclinic.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Code Coverage with JaCoCo') {
            steps {
                sh 'mvn jacoco:report'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/site/jacoco/index.html', fingerprint: true
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
}
