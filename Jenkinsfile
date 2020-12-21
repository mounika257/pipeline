pipeline {
    agent any
	tools {
        maven "MAVEN_HOME" 
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


        stage ('Install Stage') {
            steps {
                
                    sh 'mvn install'
                
            }
        }
	    stage ("sonar") {
	        steps {
                    sh ' mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent package sonar:sonar ' +
                       ' -Dsonar.host.url=http://13.233.183.172:9000 ' +
                       ' -Dsonar.login=ad3acda93d498eac904596b6c61f71919eee29b2 '
            }
	}    
    }
}
