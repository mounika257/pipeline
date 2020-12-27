node {
    def server = Artifactory.server('mounika.jfrog.io')
    def buildInfo = Artifactory.newBuildInfo()
    def rtMaven = Artifactory.newMavenBuild()
    
    
    stage ('Checkout & Build') {
        git url: 'https://github.com/mounika257/pipeline.git'
    }
	  stage ("sonar") {
	        steps {
                    sh ' mvn package org.jacoco:jacoco-maven-plugin:prepare-agent package sonar:sonar ' +
                       ' -Dsonar.host.url=http://13.233.183.172:9000 ' +
                       ' -Dsonar.login=ad3acda93d498eac904596b6c61f71919eee29b2 '
            }
	}      

    
    stage ('Artifactory configuration') {
        // Obtain an Artifactory server instance, defined in Jenkins --> Manage..:
         
        rtMaven.tool = 'MAVEN_HOME' // Tool name from Jenkins configuration
        rtMaven.deployer releaseRepo: 'example-repo-local', snapshotRepo: 'example-repo-local', server: server
        rtMaven.resolver releaseRepo: 'example-repo-local', snapshotRepo: 'example-repo-local', server: server
        rtMaven.deployer.deployArtifacts = true // Disable artifacts deployment during Maven run
     }
            
    stage ('Install') {
        rtMaven.run pom: 'pom.xml', goals: 'package', buildInfo: buildInfo
     }
 
    stage ('Deploy') {
        rtMaven.deployer.deployArtifacts buildInfo
    }
        
    stage ('Publish build info') {
        server.publishBuildInfo buildInfo
    }
    
    stage('Status Notification'){
        def mailRecipients = "mounikashetty111@gmail.com"
        def subject = "${env.JOB_NAME} - Build #${env.BUILD_NUMBER}- ${currentBuild.result}"
       
        mail bcc: '',
             from: 'mounikashetty111@gmail.com',
             to: 'mounikashetty1111@gmail.com',
             subject: subject,
             body: "Build Number: #${env.BUILD_NUMBER}  Status:${currentBuild.result} Build URL: ${env.BUILD_URL}"
          
   }  
}
