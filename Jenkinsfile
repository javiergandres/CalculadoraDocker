pipeline {
    agent any
    stages {
        stage("Compilar") {
            steps {
                sh "./gradlew compileJava"
            }
        }
        stage("Test") {
            steps {
                sh "./gradlew test"
            }
        }
	stage("Construir"){
	    steps {
		sh "./gradlew build"
		}
	}

	stage("docker contruir"){
	    steps {
	    	sh "docker build -t localhost:5000/calculadora"
	    }	
	}
	stage("docker push"){
	    steps {
	    	sh "docker push localhost:5000/calculadora"
	    }	
	}
	stage("docker borrar"){
	    steps {
	    	sh "docker rm calculadora"
	    }	
	}
	stage("docker crear contenedor"){
	    steps {
	    	sh "docker run -d - 9090:8090 calculadora localhost:5000/calculadora"
	    }	
	}
    }
}
