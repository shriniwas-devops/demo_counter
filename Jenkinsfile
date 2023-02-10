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

                        def readPomVersion = readMavenPom file: 'pom.xml'

                        def nexusRepo = readPomVersion.version.endsWith("SNAPSHOT")  ?  "mrdevopsapp-snapshot" : "mrdevopsapp-release"
                        nexusArtifactUploader artifacts: 
                        
                        [
                            [
                                artifactId: 'springboot',
                                 classifier: '', 
                                 file: 'target/Uber.jar',
                                  type: 'jar'
                                  ]
                                  ],
                                    credentialsId: 'nexus-credns',
                                    groupId: 'com.example', 
                                    nexusUrl: '13.233.89.192:8081',
                                    nexusVersion: 'nexus3',
                                    protocol: 'http',
                                    repository: nexusRepo ,
                                    version: "${readPomVersion.version}"



                    }
                

}

            }


            stage('docker image building'){

                steps{


                        script{


                            sh 'docker image build -t $JOB_NAME:v1.$BUILD.ID .'
                            sh 'docker image tag $JOB_NAME:v1.$BUILD.ID shriniwas34/$JOB_NAME:v1.$BUILD.ID'
                            sh 'docker image tag $JOB_NAME:v1.$BUILD.ID shriniwas34/$JOB_NAME:latest'


                        }



                }


            }



            stage('Push image to Dockerhub'){

    
                withCredentials([string(credentialsId: 'dockerHub_passwd', variable: 'dockerHub_passwd')]) {
    
    
                        sh 'docker login -u  shriniwas34  -p  ${dockerHub_passwd}'
                        sh 'docker image push shriniwas34/$JOB_NAME:v1.$BUILD.ID'
                        sh 'docker image push shriniwas34/$JOB_NAME:latest' 
    
                    }


                steps{


                    script{


                    }
                }
            }




        }
}
        
