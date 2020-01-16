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
     
   }
}