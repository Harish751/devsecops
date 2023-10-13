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
                ssh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@100.26.207.49:/prod/apache-tomcat-9.0.80/webapps/webapp.war'
              }      
           }       
    }
    
  }
}
  
