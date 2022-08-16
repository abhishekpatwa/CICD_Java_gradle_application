pipeline {
     agent {
             docker {
             image 'openjdk:11'
               		    }
          	    }
    environment{
        VERSION = "${env.BUILD_ID}"
    }
    stages {
          stage('Building') {
             steps {
                  sh 'chmod +x gradlew'
                  sh "./gradlew build   |  tee output.log"
                   }
                }
                stage('Monitoring the logs') {
                    steps {
                        script {
                                sh '! grep "Task" output.log'
                        }
                    }
               }
            stage('Docker build and push'){
                steps{
                    sh'''
                    docker build -t 176.34.67.226:8081/springapp:${VERSION} .
                    docker login -u admin -p $docker_password 34.125.214.226:8083 
                    docker push  176.34.67.226:8081/springapp:${VERSION}
                    docker rmi   176.34.67.226:8081/springapp:${VERSION}

                    '''
                }
            }
      }
}
