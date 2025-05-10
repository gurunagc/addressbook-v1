pipeline {

    agent any

    parameters{
        string(name:'Env',defaultValue:'Test',description:'version to deploy')
        booleanParam(name:'executeTests',defaultValue: true,description:'decide to run tc')
        choice(name:'APPVERSION',choices:['1.1','1.2','1.3'])
    }


    stages {
        stage('Compile') {
            steps {
                script{

                echo 'Compile Hello World'
                echo "Deploying in ${params.Env} environment"
                sh "mvn compile"
                }
            }
        }
        
        stage('UnitTest') {
              when{
                expression{
                    params.executeTests == true
                    script{
                    sh "mvn test"
                    }
                }
            }
            steps {
                echo 'Run UnitTest cases for  Hello World'
            }
        }
        stage('Codereview') {
            steps {
                script{

                echo 'Compile Hello World'
                echo "Deploying in ${params.Env} environment"
                sh "mvn pmd:omd"
                }
            }
        }
        stage('Codecoverage') {
            steps {
                script{

                echo 'Compile Hello World'
                echo "Deploying in ${params.Env} environment"
                sh "mvn compile"
                }
            }
        }
        stage('Package') {
            steps {
                script{
                echo 'Package Hello World'
                echo "Packaging version ${params.APPVERSION}"
                sh "mvn verify"
                }
            }
        }
        stage('publishtojfrog') {
            steps {
                script{
                echo 'Package Hello World'
                echo "Packaging version ${params.APPVERSION}"
                sh "mvn -U deploy -s settings.xml"
                }
            }
        }
    }
}

   
