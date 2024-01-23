pipeline {
    agent { node { label 'kitchensink' } } 
    stages {
        stage('Build') {
            steps {
              withMaven(maven: 'maven-3') {
                sh 'mvn -B -DskipTests clean package'
              }
            }
        }
        stage('Test') {
            steps {
              withMaven(maven: 'maven-3') {
                sh 'mvn test'
              }
            }
            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
