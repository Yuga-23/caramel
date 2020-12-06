pipeline{
    agent none
     options {
    buildDiscarder(logRotator(numToKeepStr: '3'))
  }
    stages{
        stage("Download"){
            agent{label"master"}
            steps{
                            git credentialsId: 'bc9b3ce7-a257-46ae-9d40-824f939c81d4', url: 'https://github.com/Yuga-23/caramel.git'
                         sleep 5
            }
        }
        stage("build"){
             agent{label"master"}
            steps{
                sh 'mvn package'
                sleep 5
            }
        }
        stage("archive"){
             agent{label"linux-node"}
            steps{
                // This step should not normally be used in your script. Consult the inline help for details.
archive '**/*.war'
                sleep 5
            }
        }
        stage("Deploy"){
             agent{label"linux-node"}
            steps{
                sh 'scp /home/ubuntu/workspace/yugandhar_pipeline/target/app.war  ubuntu@172.31.19.219:/home/ubuntu/appserver/yuga.war'
                sleep 5
            }
        }
        /*stage("Nexus deploy"){
            steps{
                nexusPublisher nexusInstanceId: 'releases', nexusRepositoryId: 'sampledeploy', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/home/ubuntu/workspace/yugandhar_pipeline/target/app.war']], mavenCoordinate: [artifactId: 'app', groupId: 'caramelit', packaging: 'war', version: '3.0']]]

            }
        }*/
        stage("Email"){
            steps{
                mail bcc: '', body: 'Hai yugandhar please check the job', cc: '', from: '', replyTo: '', subject: 'Every build', to: 'yugandhar.prathi@gmail.com'
                sleep 5
            }
        }
    }
}
