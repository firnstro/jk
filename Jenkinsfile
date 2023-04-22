pipeline {
    agent  any;
    stages {
        stage('Preparando el entorno') {
            steps {
                sh 'python3 -m pip install -r requirements.txt'
            }
        }
        stage('Calidad de código') {
            steps {
                sh 'python -m pylint app.py'
            }
        }
        stage('Tests') {
            steps {
                sh 'python -m pytest'
            }
        }
   
    stage('construcción del artefacto') {
          agent { 
            node{
              label "DockerServer"; 
              }
          }
          steps {
              sh 'docker build https://github.com/firnstro/jk.git -t richijenkins:latest'
          }
      }        
      stage('Despliegue') {
          agent { 
            node{
              label "DockerServer"; 
              }
          }
          steps {
              sh 'docker run -tdi --name richi -p 5000:5000 richijenkins:latest'
          }
      }
    }

}
