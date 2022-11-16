
pipeline {
          agent any
          stages{
            stage('Checkout GIT'){
                steps{
                    echo 'Pulling...';
                    git branch: 'AymenBack',
                    url : 'https://github.com/khalsibadis/devOps-Backend.git';
                }

            }
            stage('MVN CLEAN'){
            steps{
                echo 'Pulling...';
                sh 'mvn clean'
                }
            }
             stage('MVN COMPILE'){
                steps{
                sh 'mvn compile'
                }
             }
             stage('MVN PACKAGE'){
                steps{
                sh 'mvn package'
                }
             }
             stage('MVN TEST'){
                steps{
                 sh 'mvn test'
                 }
             }

              stage('MVN SONARQUBE '){
                 steps{
                    sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=esprit'
                 }
              }
              stage("nexus deploy"){
                 steps{
                  nexusArtifactUploader artifacts: [[artifactId: 'achat', classifier: '', file: '/var/lib/jenkins/workspace/DevOpsBack/target/docker-spring-boot.jar', type: 'jar']], credentialsId: 'nexus-snapshots', groupId: 'tn.esprit.rh', nexusUrl: '192.168.56.11:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'nexus-snapshots', version: '1.0.0'
                 }
              }
                stage('Build Docker Image') {
                 steps {
                 sh 'docker build -t yoser/spring:1.0.0 .'
                 }
              }

              stage('Push Docker Image') {
                   steps {
                    // withCredentials([string(credentialsId: 'DockerhubPWS', variable: 'DockerhubPWS')]) {
                    sh "docker login -u yoser -p adminadmin"
                    //  }
                     sh 'docker push yoser/spring:1.0.0'
                //    }
              }
             // stage('DOCKER COMPOSE') {
                 //  steps {
                    //  sh 'docker-compose up -d --build'
                  // }
              }
         }
              
              
