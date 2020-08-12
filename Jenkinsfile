node('master') 
{
  stage('ContinuousDownload') 
  {
      git 'https://github.com/vaishnavi972/maven.git'
  }  
  stage('ContinuousBuild') 
  {
      sh label: '', script: 'mvn package'
  }  
  stage('ContinuousDeployment') 
  {
      sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.5.113:/var/lib/tomcat8/webapps/testapp.war'
  } 
  stage('ContinuousTesting') 
  {
      git 'https://github.com/vaishnavi972/FunctionalTesting.git'
      sh label: '', script: 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline/testing.jar'
  }
  stage('ContinuousDelivery') 
  {
      input message: 'Waiting for approval from the DM!', submitter: 'Srinivas'
      sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.5.239:/var/lib/tomcat8/webapps/prodapp.war'
  } 
}
