// start of pipeline
pipeline {
  // where pipeline job will run
  agent {
    label "windows_slave"
  }
  
  // start of stages : build, test, deploy ...
  stages {
    // start of stage : build
    stage('build') {
      // start of running steps inside one stage
      steps {
        // invoke command to build with maven
        bat 'mvn clean install'
      }
    }
    
        // Publish Results
    stage('Results') {
      steps {
        junit '**/target/surefire-reports/*.xml'
      }
    } 
    
    stage('User interaction') {
      steps {
        input message: 'Do u want to continue? Proceed or Abort', ok: 'Yes'
      }
    } 
    
        // start of deploy state
    stage('deploy') {
      // define step to run
      steps {
        //invoke command to stop tomcat service
        bat 'sc stop Tomcat7'
        bat 'ping 127.0.0.1 -n 6'
        // copy war file from build target to webapp Tomcat folder
        bat 'xcopy /y C:\\jenkins_slave\\workspace\\GOL_Pipeline\\gameoflife-web\\target\\gameoflife.war "C:\\Program Files\\Apache Software Foundation\\Tomcat 7.0\\webapps"'
        //invoke command to start tomcat service      
        bat 'sc start Tomcat7'
      }
    } 
    
  } 
}

