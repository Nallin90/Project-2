node {
    def mvnHome = tool 'MyMaven'
    def dockerImageTag = "baronea90/dockerhub:project2-{env.BUILD_NUMBER}"
    stage('clone repo'){
        git 'https://github.com/Nallin90/Project-2.git'
        mvnHome = tool 'MyMaven'
    }
    stage('Build project2'){
        //sh    linux
        bat "C:\\apache-maven-3.8.5\\bin\\mvn clean install -DskipTests=true"
        //jar file will be generated
    }
    stage('Build docker image'){
        dockerImage = docker.build("baronea90/dockerhub:project2-{env.BUILD_NUMBER}")
    }
    stage('Build docker deploy'){
        echo "Docker Image Tag name : ${dockerImageTag}"
        //docker-hub-credentials - we have to create in jenkins credentials
        docker.withRegistry('https://registry.hub.docker.com','docker-hub-credentials') {
            dockerImage.push("$project2-{env.BUILD_NUMBER}")
            dockerImage.push("latest")
        }
    }
}