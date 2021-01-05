pipeline {
    agent any;
    // options {
               
    // }
    environment {

        TOMCAT_HOST_ADDRESS = "54.81.25.125"

    }
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
                sh "ls -la"
            }    
        }
        
        stage('Copy Artifact'){
            steps{

                sh "find . -name *.war"                
                sh "ls -la"
                sh "whoami"
                sh "curl -v http://${TOMCAT_HOST_ADDRESS}:8080/helloworld/ > curl.txt"

                sh "scp /tmp/hello-world.war -v ec2-user@${TOMCAT_HOST_ADDRESS}:/home/ec2-user/" 

                sh "find . -name curl.txt "
                sh "cat curl.txt"

                // sh "docker cp d6e1645e2d10: ./target/hello-world-servlet-1.1.3-SNAPSHOT.war /tmp"
                

            }
        }

        
        
    }
}
