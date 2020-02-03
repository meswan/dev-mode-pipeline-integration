node {

    try {
        stage ('Clone') {
        	checkout scm
        }
        stage ('Build') {
            sh '''
		    cd finish
		    ../scripts/test.sh

		    gradle libertyCreate
		    gradle installFeature
		    gradle deploy
            gradle libertyStart
            gradle test
            gradle libertyStop
		    cd ..
            '''
        }
        stage ('Tests') {
	        parallel 'static': {
	            sh "echo 'shell scripts to run static tests...'"
	        },
	        'unit': {
	            sh "echo 'shell scripts to run unit tests...'"
	        },
	        'integration': {
	            sh "echo 'shell scripts to run integration tests...'"
	        }
        }
      	stage ('Deploy') {
            sh "echo 'shell scripts to deploy to server...'"
      	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
