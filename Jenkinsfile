pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mvn_home"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/devopstraining042024/Java-Web-Apps.git'

                // To run Maven on a Windows agent, use
                 bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            post{
                success{
                archiveArtifacts artifacts: 'target/*.war'
                }
            }
            
        }
        // stage("build & SonarQube analysis") {
        //     agent any
        //     steps {
        //       withSonarQubeEnv('sonarqube') {
        //         bat 'mvn clean package sonar:sonar'
        //       }
        //     }
        //   }

       stage('tomcat deploy'){
           steps {
           deploy adapters: [tomcat9(credentialsId: 'tomcat_creds', path: '', url: 'http://localhost:8081/')], contextPath: null, war: 'target/*war'
           }
       }
        
    }
}
