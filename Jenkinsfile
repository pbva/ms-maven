pipeline {
    agent any

    tools {
        maven 'Maven'
    }
    stages {
      stage ('Initial') {
            steps {
              sh '''
                   echo "PATH = ${PATH}"
                   echo "M2_HOME = ${M2_HOME}"
               '''
            }
        }
        stage ('Compile') {
            steps {
                 sh 'mvn clean compile -e'
            }
        }
        stage ('Test') {
            steps {
                 sh 'mvn clean test -e'
            }
        }

        stage('SonarQube analysis') {
           steps{
                script {
                    def scannerHome = tool 'SonarQube Scanner';//def scannerHome = tool name: 'SonarQube Scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    withSonarQubeEnv('sonar') {
                      //sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=Ms-Maven -Dsonar.sources=target/ -Dsonar.host.url=http://172.18.0.3:9000 -Dsonar.login=14c09fa032024d6f0e5923c7cead79f0bcaa23f3"
                      sh "mvn sonar:sonar -Dsonar.projectKey=Ms-Maven -Dsonar.host.url=http://172.18.0.3:9000 -Dsonar.login=d4da3a7237df0a855aab348de9e21f7b1e16e21b"

                    }
                }
           }
        }
    }
}
