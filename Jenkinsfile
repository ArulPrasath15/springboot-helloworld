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
                   sh 'sudo mvn clean package'
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
