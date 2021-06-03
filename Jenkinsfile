node
{
def mavenHome = tool name: 'maven3.8.1'
stage('1. CodeClone') 
{
git credentialsId: 'Git-Credentials', url: 'https://github.com/Venza-Tech/maven-web-app'  
}
stage('2. Build') 
{
sh "${mavenHome}/bin/mvn clean package"}

stage('3. CodeQuality') 
{
sh "${mavenHome}/bin/mvn sonar:sonar"}

stage('4. UploadNexus') 
{
sh "${mavenHome}/bin/mvn deploy"}

stage('5. DeployTomcat')
{
 deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://35.183.20.240:8080/')], contextPath: null, war: 'target/*war'

sh "${mavenHome}/bin/mvn deploy"
}

stage('6. emailnotification') {
      emailext body: 'Landmark Technologies.', recipientProviders: [developers()], subject: 'Status of Build', to: 'terese.fru@gmail.com'
}
}
