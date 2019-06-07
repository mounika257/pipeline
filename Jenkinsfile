pipeline {
    agent any
	tools {
        maven "M2_HOME" 
    }

    stages {
        stage ('Compile Stage') {

            steps {
                 
                    sh 'mvn clean compile'
                
            }
        }

        stage ('Testing Stage') {

            steps {
                
                    sh 'mvn test'
                
            }
        }


        stage ('Deployment Stage') {
            steps {
                
                    sh 'mvn deploy'
                
            }
        }
    }
}
