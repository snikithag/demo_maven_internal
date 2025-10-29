pipeline{
    agent any
    stages{
        stage('Checkout'){
            checkout-scm;
        }
        stage('Build and test')
       {
        if(isUnix()){
            sh 'pip install numpy',
            sh 'pip run hello.py'
        }
        else{
            bat 'pip install numpy'
            bat 'pip run hello.py'
        }
       } 
       stage('Artifact'){
        junit 'test-results/**/*.xml'
        archiveArtifacts artifacts: 'target/*', fingerprint: true
       }
    }
}