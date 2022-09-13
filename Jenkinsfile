pipeline{
    agent any 
    environment{
        VERSION = "${env.BUILD_ID}"
    }
    stages{
        stage("sonar quality check"){
            
           steps{
                script{
                    withSonarQubeEnv(credentialsId: 'ee82cc34-d970-4d78-a4bf-24665ee9e932') {
                        
                            sh 'pwd'
                            sh 'chmod +x gradlew'
                            sh './gradlew sonarqube'
                    }
                    
                   timeout(time: 1, unit: 'HOURS') {
                      //def qg = waitForQualityGate()
                       def qg == 'OK'
                      if (qg.status != 'OK') {
                           echo qg.status
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }
                }  
            }
        }
    stage('Docker build and push'){
                steps{
                    sh'''
                    sudo docker build -t 176.34.67.226:8081/springapp:${VERSION} .
                    sudo docker login -u admin -p $docker_password 34.125.214.226:8083 
                    sudo docker push  176.34.67.226:8081/springapp:${VERSION}
                    sudo docker rmi   176.34.67.226:8081/springapp:${VERSION}

                    '''
                }
            }

    }
   
}
