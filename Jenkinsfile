pipeline {

agent {
    node {
      label 'master'
    }
  }
  
      tools {

        maven 'maven-3.8.1'
    }
    
    stages {
        
     stage('Tool version Check') {
            steps {
                echo "Hello, Maven"
                sh "mvn --version" 
            }
        }
        
    stage('SonarQube Analysis') {
      environment {
        SCANNER_HOME = tool 'SonarQube-4.6.2'
        ORGANIZATION = "demo1_maven_pipeline"
        PROJECT_NAME = "demo1_maven_pipeline"
      }
      steps {
        withSonarQubeEnv('SonarQube') {
            sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
            -Dsonar.projectKey=$PROJECT_NAME \
            -Dsonar.sources=.'''
        }
      }
    }
        
        stage("Quality Gate") {
          steps {
            timeout(time: 1, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
            }
          }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            
        }
        
        stage('Stage 2') {
            steps {
                echo 'Stage2 Hello world!'  
                echo  'Stage2 $date'
               
            }
            
        }
        
        
        stage('Stage 3') {
            steps {
                echo 'Welcome to Stage3 '  
                echo  'Stage3 '
            }
            
        }           
    }
}
