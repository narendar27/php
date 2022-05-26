node {
	def application = "myphp"
	def dockerhubaccountid = "naren27"
	stage('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		app = docker.build("${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
  }
  stage('Deploy') {
		  sh ("docker run -d -p 9000:80 -v /www/html/:/var/www/html ${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
  }
}
