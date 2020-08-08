node {
	stage('Code-checkout') {
	git 'https://github.com/swanand-hub/devops.git'
	}

	stage('Build') {
		def mvnHome = tool 'Maven_Home'
		withEnv(["MAVEN_HOME=$mvnHome"]){
		sh '"$MAVEN_HOME/bin/mvn" clean install compile validate package'
		}
	}

	stage('Deploy') {
	deploy adapters: [tomcat9(credentialsId: '38cf3fc9-2254-442e-8b48-4ec953a2b287', path: '', url: 'http://192.168.43.71:9080/')], contextPath: null, onFailure: false, war: '**/*.war'
	}
	
	stage ('send email notification') {
	emailext attachLog: true, body: '''Dear All,
	This mail is being triggered to notify you all the job is being Built.''', recipientProviders: [developers()], subject: 'Building and Packaging a Job', to: 'swanandkamble@gmail.com'
	}
}
