pipeline {
    agent any
     parameters{
        string(name:'Env',defaultValue:'Test',description:'Environment to deploy')
        booleanParam(name:'executeTests',defaultValue: true,description:'decide to run tc')
        choice(name:'APPVERSION',choices:['1.1','1.2','1.3'])

   }

    stages {
        stage('compile') {
            steps {
                echo 'compile'
                echo "Compile the code in ${params.Env}"
            }
        }
        stage('unit test') {
            when{
                expression{
                    params.executeTests=true
                }
            }
            steps{
                echo 'run unittest'
            }

        }
        stage('package') {
            steps {
                echo 'package'
                echo "Compile the code in ${params.Env}"
            }
        }
    }
}