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

                    env.AMI_TO_BUILD = input message: 'Choose AMI to build', ok: 'Release!',
                                        parameters: [choice(name:'AMI_TO_BUILD', choices: 'docker/java/nodejs', description:'Choose the AMI to build:')]

                    sh 'packer validate ${env.AMI_TO_BUILD}'
                    // def files = findFiles(glob: '*-ami.json')
                    // for (int i = 0; i < files.size(); i++) {
                    //     sh "packer validate ${files[i]}"
                    // }
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
                to: colin.but1@gmail.com
        }
    }
}
