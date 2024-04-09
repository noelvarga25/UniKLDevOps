pipeline {
    agent any
    tools {
        maven 'local_maven'
    }
    stages {
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/**/*.war'
                }
            }
        }
        stage('Deploy to tomcat server') {
            steps{
                deploy adapters: [tomcat7(credentialsId: 'df015aa5-0664-4b8a-b8ae-3f351dbc4835', path: '', url: 'http://localhost:8181/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
