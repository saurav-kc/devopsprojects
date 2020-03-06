node{
 stage('Git Checkout'){
	git branch: 'dockercicd', url: 'https://github.com/saurav-kc/devopsprojects.git'  
 }
 stage('Maven Package'){
	def mvnHome = tool name: 'maven-3', type: 'maven'
	sh "${mvnHome}/bin/mvn clean package"
 	sh 'mv target/myweb*.war target/myweb.war'
 }
 
 stage('Build Docker Imager'){
   sh 'docker build -t saurav-kc/myweb:0.0.1 .'
 }	
 stage('Push to Docker Hub'){	
	 withCredentials([string(credentialsId: 'dockerHubPwd', variable: 'dockerHubPwd')]) {	
        sh "docker login -u sauravkc14 -p ${dockerHubPwd}"	
     }	
	 sh 'docker push saurav-kc/myweb:0.0.1'	
 } 
}
