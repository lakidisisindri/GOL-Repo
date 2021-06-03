pipeline {
    agent any
    tools {
        maven "maven"
    }

    stages {
        stage('code Check in') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/lakidisisindri/GOL-Repo.git']]])
                }
                }
    stages {
        stage('Build') {
            steps {
           sh 'clean package'
               }
               }
     stages {
         stage('code Quality') {
            steps {
        withSonarQubeEnv {
           // some block
               }
               }
     stages {
        stage('publish Artifacts') {
            steps { 
             nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'gameoflife-web/target/gameoflife.war ']], mavenCoordinate: [artifactId: 'gameoflife', groupId: 'com.wakaleo.gameoflife', packaging: 'war', version: '$BUILD_NUMBER']]]
              }
               }
Post:
 success{
        junit '**/target/surefire-reports/*.xml'
      }
 failure{ 
       emailext body: '', subject: '', to: 'sisindrilakidi@gmail.com'
       }
        }
