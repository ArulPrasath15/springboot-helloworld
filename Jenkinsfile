pipeline { 
    environment { 
        registry = "arulprasath/springboot-helloworld" 
        registryCredential = 'arul-dockerhub-id' 
        dockerImage = '' 
    }
    agent any 
    
    stages { 
        
        stage('Building war') { 
           steps { 
                script { 
       
                   sh 'echo $JAVA_HOME'
                   sh 'mvn clean install'
                }
            } 
        }
		
	 stage('create git tag'){
            steps{
                sshagent (credentials: ['github-sshkey']) {
                    sh "git tag -a $GIT_TAG -m 'Version $BUILD_NUMBER'"
                    sh('git push git@github.com:ArulPrasath15/springboot-helloworld.git HEAD:$BRANCH_NAME --tag  --force')
                
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
    post{
        success{
            build job: assignment-10-deploy-pipeline', parameters: [string(name: 'BUILD_NUMBER', value: "$BUILD_NUMBER")]
        }
    }
}
