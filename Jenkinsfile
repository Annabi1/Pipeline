pipeline {
    agent any




      stages {
        
         
       
        
        stage('Build Maven') {
            steps{

                sh "mvn  clean package"
                
            }
        }
             stage('ArchiveArtifacts') {
            steps{
               sh "mvn package "
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }}
        
 stage('Deploy') {
            steps {
deploy adapters: [tomcat9(credentialsId: 'tomcatUserAnnabi', path: '', url: 'http://3.210.202.57:8080/')], contextPath: 'index', war: '**/*.war'
            }}
        
        
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t ba2aec10e58f/devops-1.0    .'
                }
            }
        }
         
        stage('Deploy Docker Image') {
            steps {
                script {
                withCredentials([string(credentialsId: 'ba2aec10e58f', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u ba2aec10e58f -p ${dockerhubpwd}'
                 }  
                 sh 'docker push ba2aec10e58f/my-app-1.0'
                }
            }
        }
         stage('Docker pull') {
            steps{

                sh "docker pull ba2aec10e58f/my-app-1.0:latest"
                
            }
        }
        
       
     
           
            }
    }

