pipeline {
	agent any
	tools {
		NodeJs 'NodeJS'
	}
	environment {
		SONAR_PROJECT_KEY = 'complete-CICD'
		SONAR_SCANNER_HOME = tool 'SonarQubeScanner'
	// 	JOB_NAME_NOW = 'cicd02'
	// 	ECR_REPO = 'iquantawsrepo'
	// 	IMAGE_TAG = 'latest'
	// 	ECR_REGISTRY = '358966077154.dkr.ecr.us-east-1.amazonaws.com'
	// 	ECS_CLUSTER = 'iquant-ecs'
	// 	ECS_SERVICE = 'iquant-ecs-svc'
	// 	ALB_TARGET_GROUP_ARN = 'ecs-iquant-svc-tg'
	}
	stages {
		stage('GitHub'){
			steps {
				git branch: 'main', credentialsId: 'jenkins-sonarqube', url: 'https://github.com/hossain109/Complete-CI-CD.git'
			}
		}
		stage('Unit Test'){
			steps {
				sh 'npm test'
				sh 'npm install'		
			}
		}
		stage('SonarQube Analysis'){
			steps {
				withCredentials([string(credentialsId: 'sonar-credential', variable: 'SONAR_TOKEN')]) {
					withSonarQubeEnv('SonarQube') {
					// some block
					}

				}	
					withSonarQubeEnv('SonarQube') {
    						sh """
						${SONAR_SCANNER_HOME}/bin/sonar-scanner \
						-Dsonar.projectKey=${SONAR_PROJECT_KEY} \
						-Dsonar.sources=. \
						-Dsonar.host.url=http://sonarqube-dind:9000 \
						-Dsonar.login=${sonar-token}
						"""
					}
			}
		}
		// stage('Docker Image'){
		// 	steps {
		// 		script {
		// 			docker.build("${ECR_REGISTRY}/${ECR_REPO}:${IMAGE_TAG}")
		// 		}
		// 	}
		// }
		// stage('Login to ECR'){
		// 	steps {
		// 		sh """
		// 		aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 358966077154.dkr.ecr.us-east-1.amazonaws.com
		// 		"""
		// 	}
		// }
		// stage('Push Image to ECR'){
		// 	steps {
		// 		script {
		// 		docker.image("${ECR_REGISTRY}/${ECR_REPO}:${IMAGE_TAG}").push()
		// 		}
		// 	}
		// }
	}
}