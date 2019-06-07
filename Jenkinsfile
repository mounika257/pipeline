pipeline {
    agent any
	tools {
        maven "M2_HOME" 
    }

    stages {
        stage ('Compile Stage') {

            steps {
                 
                    bat 'mvn clean compile'
                
            }
        }

        stage ('Testing Stage') {

            steps {
                
                    bat 'mvn test'
                
            }
        }


        stage ('Install Stage') {
            steps {
                
                    bat 'mvn install'
                
            }
        }
    }
}
