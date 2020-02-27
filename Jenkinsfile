node{
	stage('SCM Checkout'){
		git branch: 'wartomcat', url: 'https://github.com/saurav-kc/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'maven-3.5.4', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['tomcat-dev']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@54.89.177.80:/opt/tomcat9/webapps/'
	}
	stage('Slack Notification'){
                 slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#jenkinsnotification', color: '#439F30', message: 'New build deploy test', teamDomain: 'intelycoreworkspace', tokenCredentialId: 'slack-secret'	
	}
}
