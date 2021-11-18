pipeline { 
    environment { 
        registry = "arulprasath/springboot-helloworld" 
        registryCredential = 'arul-dockerhub-id' 
        dockerImage = '' 
    }
    agent any 
    
    stages { 
        
        stage('mvn clean') { 
           steps { 
                script { 
       
                   sh 'echo $JAVA_HOME'
                   sh 'mvn clean install'
                }
            } 
        }
        
         stage('Building springboot image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry 
                }
            } 
        }
        
        stage('Push image to docker hub') { 
            steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push("build-$BUILD_NUMBER") 
                    }
                } 
            }
        } 
            
    }
}
