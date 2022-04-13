//Owen Anderchek, A01211852
//13/04/2022
//Pipeline to run sample code for final exam

pipeline {
    agent any
    environment {
        TARGET = ""
    }
    stages {

        stage('Build') {
            steps{
                sh 'echo Running the Requirements'
                sh 'pip install -r requirements.txt'
                sh 'echo Requirements Complete!'
            }
        }
        stage('Code Quality') { 
            steps {
                sh 'pylint-fail-under --fail_under 7.0 *.py'
            } 
        } 
        stage("Code Quantity") {
            steps {
                sh 'wc -l *.py'
            }
        }       
      //make this work and maybe take out the params.DEPLOY
         stage("Run Scripts") {
            when { ${TARGET} == "run" }
            steps {
                sh 'python main.py phone text output'
                sh 'python main.py tablet csv output'
                sh 'python main.py laptop json output'
            }
         }
        stage("Zip") {
            steps {
                sh "echo 1"
            }
        }
    }
}
