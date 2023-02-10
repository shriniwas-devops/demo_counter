pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/shriniwas-devops/demo_counter.git'
                }
            }
        }
        stage('UNIT testing'){
            
          steps{
                
             script{
                    
                 sh 'mvn test'
        }
        }
        }
        stage('Integration testing'){
            
             steps{
                
                script{
                    
                   sh 'mvn verify -DskipUnitTests'
                 }
            }
         }
        stage('Maven build'){
            
           steps{
                
             script{
                    
                  sh 'mvn clean install'
               }
           }
         }
        stage('Static code analysis'){
            
          steps{
                
              script{
                    
                 withSonarQubeEnv(credentialsId: 'sonar-token') {
                        
                     sh 'mvn clean package sonar:sonar'
                }
                 }
       
             }
         }
            stage('Quality Gate Status'){
                
               steps{
                    
                 script{
                        
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
              }
            }


            stage('Nexus Artifact uploader'){


                steps{


                    script{


                            nexusArtifactUploader artifacts:
                             [
                                [
                                    artifactId: 'springboot', 
                                    classifier: '', 
                                    file: 'target/Uber.jar',
                                     type: 'jar'
                                     ]
                                     
                                     ],
                                    credentialsId: 'nexus-creds', 
                                    groupId: 'com.example',
                                    nexusUrl: '13.233.89.192:8081',
                                    nexusVersion: 'nexus3', 
                                    protocol: 'http',
                                     repository: 'shridevops-release'
                                     version: '1.0.0'



                    }

}

            }




        }
}
        
