pipeline {
    agent any

    stages {
        stage('compile') {
            steps {
                echo 'compile'
            }
        }
        stage('CodeReview') {
            agent any
            steps {
                echo 'test'
            }
        }
        stage('package') {
            steps {
                script{
                    echo "UnitTest in junit"
                    sh "mvn test"
                }
                
            }
            post{
                always{
                    junit 'target/surefire-reports/*.xml'
                }
            }
            
        }
        stage('CodeCoverage') {
            agent {label 'linux_slave'}
            steps {
                script{
                    echo "Code Coverage by jacoco"
                    sh "mvn verify"
                }
                
            }
            
        }
        stage('Package') {
            agent any
            input{
                message "Select the platform for deployment"
                ok "Platform Selected"
                parameters{
                    choice(name:'Platform',choices:['EKS','EC2','On-prem'])
                }
            }
            steps {
                script{
                    sshagent(['slave2']) {
                    echo "packaging the code"
                    echo 'platform is ${Platform}'
                    echo "packing the version ${params.APPVERSION}"
                    //sh "mvn package"
                    sh "scp  -o StrictHostKeyChecking=no server-script.sh ${BUILD_SERVER}:/home/ec2-user"
                    sh "ssh -o StrictHostKeyChecking=no ${BUILD_SERVER} 'bash ~/server-script.sh'"
                    
                }
                
            }
            
        }
    }
}
}
