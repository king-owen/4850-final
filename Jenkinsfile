//Owen Anderchek, A01211852
//13/04/2022
//Pipeline to run sample code for final exam

pipeline {
    agent any
    environment {
        TARGET = "run"
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
         stage("Run Scripts") {
            when { 
                environment name: 'TARGET', value: 'run' 
            }
            steps {
                sh 'python3 main.py phone text output'
                sh 'python3 main.py tablet csv output'
                sh 'python3 main.py laptop json output'
            }
         }
        stage("Zip") {
            steps {
                script {
                sh "zip final.zip *.py"
                sh "echo Owen Anderchek"
                sh "echo A01211852"
            }
            archiveArtifacts artifacts: 'final.zip'
            }
        }
    }
}
