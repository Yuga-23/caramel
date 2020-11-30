pipeline{
    agent any
    stages{
        stage("Download"){
            steps{
                            git credentialsId: 'bc9b3ce7-a257-46ae-9d40-824f939c81d4', url: 'https://github.com/Yuga-23/caramel.git'

            }
        }
        stage("build"){
            steps{
                sh 'mvn package'
            }
        }
        stage("archive"){
            steps{
                // This step should not normally be used in your script. Consult the inline help for details.
archive '**/*.war'
            }
        }
        stage("Deploy"){
            steps{
                sh 'scp /var/lib/jenkins/workspace/yugandhar_pipeline/target/app.war  ubuntu@172.31.19.219:/home/ubuntu/appserver/yuga.war'
            }
        }
        stage("Nexus deploy"){
            steps{
                nexusPublisher nexusInstanceId: 'releases', nexusRepositoryId: 'sampledeploy', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/lib/jenkins/workspace/yugandhar_pipeline/target/app.war']], mavenCoordinate: [artifactId: 'app', groupId: 'caramelit', packaging: 'war', version: '3.0']]]

            }
        }
        stage("Email"){
            steps{
                mail bcc: '', body: 'Hai yugandhar please check the job', cc: '', from: '', replyTo: '', subject: 'Every build', to: 'yugandhar.prathi@gmail.com'
            }
        }
    }
}
