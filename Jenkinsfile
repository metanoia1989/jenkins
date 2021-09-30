// Jenkinsfile (Declarative Pipeline)
pipeline{
    agent{
        docker {
            image 'php'
        }
    }
    stages{
        stage("build"){
            steps{
                sh 'php --version'
                echo "========executing get php version========"
            }
        }
    }
}