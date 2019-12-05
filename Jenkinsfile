pipeline {
    agent {
        docker {
            image 'packer-build:latest'
        }
    }
    stages {
        stage ('validate template') {
            steps {
                script {
                    def files = findFiles(glob: '*-ami.json')
                    for (int i = 0; i < files.size(); i++) {
                        sh "packer validate ${files[i]}"
                    }
                }
            }
        }
        stage ('build template') {
            steps {
                when ('master') {
                    sh 'packer build microservice-docker-ami.json'
                }
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
