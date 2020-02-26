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
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@54.235.225.106:/opt/tomcat9/webapps/'
	}
	}
}
