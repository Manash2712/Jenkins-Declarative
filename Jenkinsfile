pipeline{
  agent any
  stages{
    stage('Git Checkout'){
      steps{
        git 'https://github.com/Manash2712/myweb'
      }
    }
    stage('Maven build'){
      steps{
        sh 'mvn clean package'
        sh 'mv target/*war target/myweb.war'
      }
    }
    stage('Deploy-Dev'){
      steps{
        sshagent(['dev-server']) {
            sh """
              scp -o StrictHostKeyChecking=no /target/myweb.war ec2user@172.31.12.214:/var/lib/tomcat9/webapps/ 
              ssh ec2user@172.31.12.214 systemctl restart tomcat9
            """"
        }
      }
    }
  }
}
