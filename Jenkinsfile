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
                    env.AMI_TO_BUILD = input message: 'Choose AMI to build', ok: 'Build!',
                                        parameters: [choice(name:'AMI_TO_BUILD', choices: 'docker\njava\nnodejs', description:'Choose the AMI to build:')]
                    sh "packer validate microservice-${env.AMI_TO_BUILD}-ami.json"
                }
            }
        }
        stage ('build template') {
            when { 
                branch 'master' 
            }
            steps {
                sh 'packer build microservice-docker-ami.json'
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
        always {
            emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
                to: "colin.but1@gmail.com"
        }
    }
}
