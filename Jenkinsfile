pipeline {
    agent {
        docker {
            image 'packer-build'
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
