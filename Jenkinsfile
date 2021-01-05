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
        
        stage('Deploy'){
            steps{
                
                sh "find . -name *.war"


                // sh (label: "Create EC2", script: '''       
                //     aws ec2 run-instances \
                //         --image-id ami-04d29b6f966df1537 \
                //         --count 1 \
                //         --instance-type t2.micro \
                //         --key-name new_nvirginia \
                //         --security-group-ids sg-09536172f769fe814 \
                //         --subnet-id subnet-38f37067 \
                //         --user-data file:///home/usov/solutions/ud.txt \
                //         --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=Tomcat},{Key=owner,Value=Reagan}]'
                // ''')
                script{
                 
                    TOMCAT_HOST_ADDRESS = sh (returnStdout: true, script: '''
                        aws ec2 describe-instances \
                            --filters 'Name=tag:Name,Values=Tomcat' \
                            --query 'Reservations[].Instances[].PublicIpAddress[]' \
                            --output text

                    ''')
                }

                sshagent(credentials: ['new_nvirginia']) {
                    sh (label: "Deploy App", script: "scp target/hello-world-servlet-1.1.3-SNAPSHOT.war -v ec2-user@${TOMCAT_HOST_ADDRESS}:/apache-tomcat-9.0.41/webapps")                                      
                }
                sh "find . -name *.xml"
                sh "ls -la"
            }    
        }
        
        stage('Test'){
            steps{

                sh "find . -name *.war"                
                sh "ls -la"

             
                sh ( label:'Test', script:"curl -I -s http://${TOMCAT_HOST_ADDRESS}:8080/helloworld/ | grep -q 'HTTP/1.1 200' ") 
                

                

             //   sh "scp /tmp/hello-world.war -v ec2-user@${TOMCAT_HOST_ADDRESS}:/tmp" 

                
                

                // sh "docker cp d6e1645e2d10: ./target/hello-world-servlet-1.1.3-SNAPSHOT.war /tmp"
                

            }
        }

        //  stage('List S3 buckets') {
        //     withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'new_nvirginia', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        //         AWS("--region=eu-east-1 s3 ls")
        //      }
        //  }
        
    }
}
