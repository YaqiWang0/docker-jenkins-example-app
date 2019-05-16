node{
	try{
        def app
	
	stage('clone repository'){
		checkout scm
	}
	stage('build image'){
		app =docker.build('quay.io/emmawang9506/example-app')
	}
	stage('Test'){
		app.inside{
			sh 'npm test'
		}
	}
	stage('Push Image'){
		docker.withRegistry('https://quay.io','quay-io-credentials'){
			 app.push("${env.BRANCH_NAME}-latest")
                         app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
		}
	}
	}catch(error){
                withCredentials([[$class: 'StringBinding', credentialsId: 'slack-webhook-url', variable: 'SLACK_URL']]){
		sh "curl -XPOST -d 'payload={ \"color\":\"danger\",\"text\":\"warning: Build failed: $error (see<${env.BUILD_URL}/console|the build logs>)\" }' ${env.SLACK_URL}"
	}        
	}
}
