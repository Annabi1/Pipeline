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
deploy adapters: [tomcat9(credentialsId: 'tomcatUserAnnabi', path: '', url: 'http://3.238.39.47:8080/')], contextPath: 'index', war: '**/*.war'
            }}
        
        
        stage('Build   Dockerfile ') {
            steps {
                script {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'DockerServer', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''docker stop docker_demo;
docker rm -f docker_demo;
docker image rm -f docker_demo;
cd /opt/docker;
docker build -t docker_demo .
docker run -d --name docker_demo -p 8090:8080 docker_demo
''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//docker', remoteDirectorySDF: false, removePrefix: 'webapp/target', sourceFiles: 'webapp/target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                }
            }
        }
         
          
         
     
           
            }
    }

