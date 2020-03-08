node
{
    def mavenHome=tool name: "maven3.6.3"
    stage('checkout')
    {
    git branch: 'development', credentialsId: 'ca047832-5650-4d70-af26-37ed10a2bc48', url: 'https://github.com/Madhu-Kart-org/maven-web-application.git'
     }
     
     stage('build')
    
     {
         sh "${mavenHome}/bin/mvn clean package"
     }
     
     stage('SQreport')
    
     {
         sh "${mavenHome}/bin/mvn clean sonar:sonar"
     }
     
          stage('uploadArtifacts')
    
     {
         sh "${mavenHome}/bin/mvn clean deploy"
     }
     
     stage('tomcat')
     {
         sshagent(['2828b2ab-40ca-4c40-a93e-ec9baadbba9c']) {
         sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.78.144:/opt/apache-tomcat-7.0.100/webapps/"
         }
     }
}
