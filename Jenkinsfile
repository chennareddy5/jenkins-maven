pipeline { 
    agent any 
    tools {
    maven "Maven"
  }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
       stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
        stage('sonar quality check'){
            steps{
                withSonarQubeEnv('sonar'){
                    sh "mvn sonar:sonar \
                -Dsonar.projectKey=jenkins-sonar-integration \
                -Dsonar.host.url=http://3.109.108.203:9000/"
                    }
            }
        }
        
                   
    }
    
}
