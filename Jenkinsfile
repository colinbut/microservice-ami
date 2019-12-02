pipeline {
    agent {
        docker {
            image 'packer-build'
        }
    }

    stages {
        stage ('validate template') {
            steps {
                sh 'packer validate microservice-java-ami.json'
            }
        }
    }

    post {
        success {
            echo "====++++Build Success!++++===="
        }
        failure {
            echo "====++++Build Failed!++++===="
        }
        unstable {
            echo "====++++Build Unstable++++===="
        }
    }
}
