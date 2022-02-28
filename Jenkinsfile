pipeline {
    agent any
    environment {
        PATH = "/usr/share/maven/bin:$PATH"
        DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }
    stages {
        stage('Init') {
            steps {
            script{
                 try{
                       sh "docker image rm -f milestone-tomcat:v1"
                       sh "docker image rm -f liveorlike/milestone-tomcat:v1"
                 }catch(error)
                 {
                      echo "No problems"
                 }
                 }
            }
        }
//         stage('Code Security'){
//                         parallel{
//                             stage('OWASP Dependency-Check Vulnerabilities'){
//                                 steps{
//                                       sh 'mvn dependency-check:check'
//                                       dependencyCheckPublisher pattern: 'target/dependency-check-report.xml'
//                                 }
//                             }
//                             stage('Sonacube'){
//                                   steps{
//                                        withSonarQubeEnv('sonarqube_server') {
//                                        sh 'mvn sonar:sonar'
//                                         }
//                                   }
//                             }
//                         }
//          }

//          stage('Build and push on Tomcat server local'){
//                                  parallel{
//                                      stage('Build') {
//                                                  steps {
//                                                      sh 'mvn clean install'
//                                                  }
//                                      }
//                                       stage('Push file tomcat server') {
//                                                  steps {
//                                                     sh 'sudo  cp target/milestone.war /opt/tomcat/webapps/'
//                                                  }
//                                       }
//                                  }
//          }
//          stage('DAST OWASP ZAP '){
//                      steps{
//                          sh 'echo "Check OWASP ZAP"'
// //                          sh 'sudo docker run --rm -u root:root -v $(pwd):/zap/wrk/:rw -t owasp/zap2docker-stable zap-baseline.py -t http://10.0.3.132:8081/milestone/ -g gen.cof  -r report.html'
//                      }
//          }
         stage('Docker'){
                                 parallel{
                                     stage('Build') {
                                                 steps {
                                                     sh 'docker build -t milestone-tomcat:v1 -f Dockerfile . '
                                                 }
                                     }
                                      stage('Login') {
                                                 steps {
                                                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                                                 }
                                      }

                                 }
         }
          stage('Push') {
                                                          steps {
                                                             sh 'docker tag milestone-tomcat:v1 liveorlike/milestone-tomcat:v1'
                                                             sh 'docker push liveorlike/milestone-tomcat:v1'
                                                          }
          }

        //  stage('Deploy on K8S'){
        //                      steps{
        //                       kubernetesDeploy(configs:"tomcatweb_k8s.yaml",kubeconfigId:"azure-kubeconfig")

        //                       }
        //  }



    }


}

