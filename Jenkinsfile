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
	    	sh "sudo docker build -t localhost:5000/calculadora ."
	    }	
	}
	stage("docker push"){
	    steps {
	    	sh "sudo docker push localhost:5000/calculadora"
	    }	
	}
	stage("borrar contenedor") {
            when {
                expression { sh script: '''if [ -z $(sudo docker ps -a -f name=calculadora -q) ]; 				then true; else false; fi''', returnStatus: true
                  }
              }
            steps {
                sh "sudo docker stop calculadora"
                sh "sudo docker rm calculadora"
             }
        }
	stage("docker crear contenedor"){
	    steps {
	    	sh "sudo docker run -d -p 9090:8090 --name calculadora localhost:5000/calculadora"
	    }	
	}
	stage("produccion") {
	    steps {
		sh "sudo ansible-playbook playbook.yml"
	    }
	}
    }
}
