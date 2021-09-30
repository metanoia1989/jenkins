// Jenkinsfile (Declarative Pipeline)
pipeline{
    agent{
        docker {
            image 'php'
        }
        any
    }
    stages{
        stage("build"){
            steps{
                sh 'php --version'
                echo "========executing get php version========"
            }
            
            steps {
                sh 'echo "hello world"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Fail!"; exit 1'
            }    
        }
        
        // 超时 重试
        stage("Deloy"){
            steps{
                retry(3) {
                    echo "====++++executing Deloy++++===="
                }
                timeout(time: 3, unit: 'SECONDS') {
                    echo "====++++health-check++++===="
                }
            }
            
            steps {
                timeout(time: 3, unit: 'SECONDS') {
                    retry(5) {
                        echo "./flakey-deloy.sh" 
                    }
                }     
            }
        }
        
    }
    
    // 完成执行后的清理阶段
    post {
         always {
             echo 'This will always run'
         }
         
         success {
             echo 'This will run only if successful'
         }
         
         failure {
             echo 'This wll run only if failed'
         }
         
         unstable {
             echo 'This will run only if the run was marked as unstable'
         }
         
         changed {
             echo 'This will run only if the state of the Pipleline has changed'
             echo 'For example, if the Pipeline was previously failing but is now successful'
         }
    }
}
