pipeline {
    agent any

	environment {
		DOCKERHUB_CREDENTIALS = credentials('dockerhub-accstoken')
		PATH = "/opt/apachemaven/bin:$PATH"
	}
	
	stages {
		//stage('Initialise') {
		//	steps {
		//		echo "PATH = ${M2_HOME}/bin:${PATH}"
		//		echo "M2_HOME = /opt/maven"
		//	}
		//}
		stage('Build Java') {
			steps {
					sh 'echo "Building JAVA Project...."'
					sh 'mvn -B -DskipTests clean package'
					sh 'echo "Jar file generated in the target folder....."'
			}
		}
		stage('Build Docker Image') {
			steps {
					sh 'echo "Building Docker Image...."'
					sh 'docker build -t jaggu199/javaapp:${BUILD_NUMBER} .'
					sh 'echo "Docker Image built successfully...."'
			}
		}
		stage('Push Docker Image') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
				sh 'docker push jaggu199/javaapp:${BUILD_NUMBER}'
			}
		}
	}
}