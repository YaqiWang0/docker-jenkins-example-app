node{
	def app
	
	stage('clone repository){
		checkout scm
	}
	stage('build image'){
		app =docker.build('yaqiwang9506/example-app')
	}
	stage('Push Image'){
		docker.withRegistry('https://registry.hub.docker.com','docker-hub-credentials'){
			app.push('latest')
		}
	}
}
