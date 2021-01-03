pipeline {
    agent any;
    // options {
        
        
        
    // }
    stages{
        stage('Show Artifact Dir'){
            steps{
                
                copyArtifacts(projectName: 'hello-world-servlet/master');
                sh "pwd"
                sh "ls -lah"                
                
            }    
        }
        
        stage('Show Artifact'){
            steps{
                
                sh "find . -name *.war"
                sh "find . -name *.xml"
                
            }    
        }
        
        stage('Copy Artifact'){
            steps{

                sh "find . -name *.war"                
                
                sh "curl -v http://54.81.25.125:8080/helloworld/ > curl.txt"
                sh "find . -name curl.txt "
                
                // sh "docker cp d6e1645e2d10: ./target/hello-world-servlet-1.1.3-SNAPSHOT.war /tmp"
                

            }
        }

        
        
    }
}
