pipeline {

    agent {
        docker {
            image 'node:latest' 
            args '-p 3000:3000' 
		}
        }

    stages {
        stage('Build') { 
            steps {
                echo 'building'
                sh 'npm install'
                
            }
            post {
        	failure {
            		emailext attachLog: true,
                	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                	to: 'stawarskimichal1@gmail.com',
                	subject: "build failed"
        	}
        	success {
            		emailext attachLog: true,
                	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                	to: 'stawarskimichal1@gmail.com',
                	subject: "build succeed"
        	}
    		}
        }

        stage('Test') { 
            steps {
                echo 'testing..'
                sh 'npm run test'
            }
            post {
		failure {
            		emailext attachLog: true,
                	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                	to: 'stawarskimichal1@gmail.com',
                	subject: "tests failed"
        	}
        	success {
            		echo 'tests succeed'
		}
    		
        	}
	}

	stage('Deploy') {
            steps {
                echo 'deploying..'
                sh 'docker build -t deploy -f Dockerfile-deploy .'
            }
            post {
        	failure {
            		emailext attachLog: true,
                	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                	to: 'stawarskimichal1@gmail.com',
                	subject: "deploy failed"
        	}
        	success {
            		emailext attachLog: true,
                	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                	to: 'stawarskimichal1@gmail.com',
                	subject: "deploy succeed"
        	}
    		}
        }
    }

}
