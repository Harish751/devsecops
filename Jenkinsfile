pipeline{
  agent any
   tools{
     maven 'Maven'
}
  stages{
         stage('Initialize'){
           steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }        
         }
 stage ('Source Composition Analysis') {
      steps {
         sh 'rm owasp* || true'
         sh 'wget "https://raw.githubusercontent.com/cehkunal/webapp/master/owasp-dependency-check.sh" '
         sh 'chmod +x owasp-dependency-check.sh'
         sh 'bash owasp-dependency-check.sh'
         sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
        
      }
    }
        stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
     stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
      
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@184.73.128.69:/home/ubuntu/prod/apache-tomcat-10.1.14/webapps/webapp.war'
              }      
           }       
    }
    
  }
}
  
