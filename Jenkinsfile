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

        stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
     stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                 sh 'ssh -o StrictHostKeyChecking=no ubuntu@54.89.124.184'
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@54.89.124.184:/prod/apache-tomcat-9.0.80/webapps/webapp.war'
              }      
           }       
    }
    
  }
}
  
