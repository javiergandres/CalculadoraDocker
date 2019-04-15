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
    }
}
