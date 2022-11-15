
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
                  nexusArtifactUploader artifacts: [[artifactId: 'tpAchatProject', classifier: '', file: '/var/lib/jenkins/workspace/projetDevops/target/docker-spring-boot.jar', type: 'jar']], credentialsId: 'nexus-snapshots', groupId: 'com.esprit.examen', nexusUrl: '192.168.33.166:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'nexus-snapshots', version: '2.2.4'
                 }
              }
         }
              }
