node{
    def mavenHome = tool name: "maven3.8.4"
    //checkout stage
    stage('checkout'){
    git branch: 'development', credentialsId: '0aedc6ca-9609-4826-88dc-fcfac2d2323d', url: 'https://github.com/mss-jan-batch-devops/maven-web-application.git'
    }
    //Build stage
    stage('Build'){
        sh "$mavenHome/bin/mvn clean package"
    }
    //Generate SonarQube Report
    stage('SonarQube Report'){
        sh "$mavenHome/bin/mvn sonar:sonar"
    }
    //Upload Artifact into Artifactory repo
    stage('Upload Artifacts into Nexus'){
        sh "$mavenHome/bin/mvn deploy"
    }
    //Deploy App into Tomcat server
    stage('Deploy App into Tomcat'){
        sshagent(['e72b67ba-051c-4d82-be15-678945866d6f']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.110.51.102:/opt/apache-tomcat-9.0.59/webapps"
}
    }
}//Node closing 
