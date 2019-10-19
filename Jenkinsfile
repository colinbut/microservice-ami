pipeline {
    agent any

    stages {
        stage ('validate template') {
            steps {
                sh 'packer validate -color=false ami.json'
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
