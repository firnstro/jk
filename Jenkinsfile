pipeline {
    agent any;
        
    stages {
        stage('info'){
            steps {
                sh 'echo $PATH'
                sh 'id'
                sh 'whoami'
                sh 'echo $HOME'
                sh 'apt install python3 python3-pip -y'
            }
        }
        stage('Preparando el entorno') {
            steps {
                sh 'python3 -m pip install -r requirements.txt'
            }
        }
        stage('Calidad de código') {
            steps {
                sh 'python3 -m pylint app.py'
            }
        }
        stage('Tests') {
            steps {
                sh 'python3 -m pytest'
            }
        }
   
    stage('construcción del artefacto') {
          agent { 
            node{
              label "test"; 
              }
          }
          steps {
              sh 'docker build https://github.com/firnstro/jk.git -t richijenkins:latest'
          }
      }        
      stage('Despliegue') {
          agent { 
            node{
              label "test"; 
              }
          }
          steps {
              sh 'docker run -tdi --name richi -p 5000:5000 richijenkins:latest'
          }
      }
    }

}
