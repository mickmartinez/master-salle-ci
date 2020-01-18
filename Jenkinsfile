pipeline {
   agent any
   stages {
      stage('Compile & Test') {
         steps {
               echo 'Hello From Jenkinsfile'
               git 'https://github.com/mickmartinez/master-salle-ci.git'
               bat 'mvn compile test'
               junit 'target/surefire-reports/*.xml'
         }
      }
      stage('Package') {
         steps {
            echo "Building $version"
            bat 'mvn package -DskipTests'
         }
      }
      stage('Acceptance Test'){
         steps{
            echo 'Executing Acceptance Test'
            bat 'mvn -Dtest=ExampleResourceIT test'
            junit 'target/surefire-reports/*.xml'
         }
      }
      stage('Staging'){
         steps{
            echo 'Deploying to pre-production environment'
            bat 'docker rm -f greetings_app_staging || true'
            bat 'docker build -f src/main/docker/Dockerfile.jvm -t quarkus/code-with-quarkus-jvm .'
            bat 'docker run --name greetings_app_staging -i --rm -p 9090:8080 quarkus/code-with-quarkus-jvm'
         }
      }
      stage('Production'){
         steps{
            echo 'Deploying to production environment'
            bat 'docker rm -f greetings_app || true'
            bat 'docker build -f src/main/docker/Dockerfile.jvm -t quarkus/code-with-quarkus-jvm .'
            bat 'docker run --name greetings_app -i --rm -p 5000:8080 quarkus/code-with-quarkus-jvm'
         }
      }
   }
}