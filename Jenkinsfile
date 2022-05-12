pipeline{
agent {label 'devserver2'}

triggers {
        pollSCM '* * * * *'
    }
stages{

stage('scm'){
steps{
checkout([$class: 'GitSCM', branches: [[name: '*/feat01']], extensions: [], userRemoteConfigs: [[credentialsId: 'd40f0185-bcfe-408d-80f3-29e353e13680', url: 'https://github.com/N-Virgina/mavenrepo.git']]])
}
}

stage('buid'){
steps{
sh 'mvn package'
}
}

stage('sonar'){
steps{
withSonarQubeEnv('sonarqube') {
    sh 'mvn sonar:sonar'
}
}
}

stage('nexus'){
steps{
sh 'mvn deploy'
}
}

stage('tomcat'){
steps{
sh 'scp /root/workspace/sample/target/studentapp-2.1.1-FEAT01-SNAPSHOT.war root@100.24.9.49:/var/lib/tomcat/webapps'
}
}

}
}
