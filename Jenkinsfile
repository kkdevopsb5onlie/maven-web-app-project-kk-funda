node
{
    def mavenHome=tool name: "maven3.9.9"
	stage('git checkout')
	{
      git branch: 'development', credentialsId: '8d341570-e046-4d2c-8060-33c3d5d493f7', url: 'https://github.com/gangavaramdevops/maven-web-app-project-kk-funda.git'
	}
	stage('compile')
	{
    sh  "${mavenHome}/bin/mvn compile"
	}
	stage('Build')
	{
    sh  "${mavenHome}/bin/mvn clean package"
	}
   stage('SQ Report')
	{
    sh  "${mavenHome}/bin/mvn sonar:sonar"
	}
	stage('Deploy into Nexus')
	{
    sh  "${mavenHome}/bin/mvn clean deploy"
	}
	stage('Deploy to Tomcat') {
        echo "Deploying WAR file using curl..."

        sh """
            curl -u kkfunda:kkfunda \
            --upload-file /var/lib/jenkins/workspace/jio-scripted-way-pipeline-develoment/target/maven-web-application.war \
            "http://3.108.194.157:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """
    }


} //node closing
