//scripted way pipeline
node
{
// var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven/-->this one can be replaced by mavenhome

def mavenHome=tool name: "maven"   

stage ('git checkout')
{

git branch: 'dev', url: 'https://github.com/NaveenDevops77/maven-webapplication-project-kkfunda.git'

}

stage ('compile')
{

sh "${mavenHome}/bin/mvn compile"

}

stage ('build')

{
sh "${mavenHome}/bin/mvn clean package"
}

stage ('sq report')
{
sh "${mavenHome}/bin/mvn clean install sonar:sonar"

}
stage ('deply nexus')
{
sh "${mavenHome}/bin/mvn clean deploy"
}
stage('Deploy to Tomcat') {
    withCredentials([usernamePassword(
        credentialsId: 'tomcat-cred', 
        usernameVariable: 'TOMCAT_USER', 
        passwordVariable: 'TOMCAT_PASS'
    )]) {

        sh """
        curl -u $TOMCAT_USER:$TOMCAT_PASS -T target/*.war "http://13.235.51.32:8080/manager/text/deploy?path=/myapp&update=true"
        """
    }
}
