node
{
    stage ('git checkout')
    {
        git branch: 'dev', url: 'https://github.com/NaveenDevops77/maven-webapplication-project-kkfunda.git'
    }
    stage('Build') {
        try {
            sh 'mvn clean package'
        }
        catch (Exception e) {
            echo "Build failed but pipeline continues"
        }
    }
    stage('Next Step') {
        sh 'echo continuing workflow'
    }
    stage ('sonar report')
    {
        sh "${mavenHome}/bin/mvn clean package sonar:sonar"
    }
    stage ('backup')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage ('upload to tomcat')
    {
    sh """
    curl -u naveen:Charish@9101112\
    --upload-file /var/lib/jenkins/workspace/java-scripted-way-pipeline/target/maven-web-application.war\
    "http://3.110.181.253:8080//manager/text/deploy?path=/maven-web-application&update=true"
     """
    }
}

