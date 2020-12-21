pipeline {
    agent any
	tools {
        maven "MAVEN_HOME" 
    }
       rtServer (
    id: 'mounika.jfrog.io',
    url: 'https://mounika.jfrog.io/artifactory',
    // If you're using username and password:
    username: 'mounikashetty111@gmail.com',
    password: 'Saibaba@257',
    // If you're using Credentials ID:
    timeout: 300
       )

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
	    stage("upload") {
		    steps{
	             rtUpload (
    serverId: 'mounika.jfrog.io',
    spec: '''{
          "files": [
            {
              "pattern": "/*.jar",
              "target": "artifactory/example-repo-local"
            }
         ]
    }''',
 
    // Optional - Associate the uploaded files with the following custom build name and build number,
    // as build artifacts.
    // If not set, the files will be associated with the default build name and build number (i.e the
    // the Jenkins job name and number).
    buildName: 'holyFrog',
    buildNumber: 'latest'
)
	    }
	}   
    }
}
