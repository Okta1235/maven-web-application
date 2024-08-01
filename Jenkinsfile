node{

def mavenhome= tool name: 'Maven3.9.8'
echo "the job name is: ${env.JOB_NAME}"

stage('checkoutcode'){
git branch: 'development', credentialsId: '426500b5-05e2-4723-a5f3-0c9f21461aab', url: 'https://github.com/Okta1235/maven-web-application.git'
}
stage('build'){
sh "${mavenhome}/bin/mvn clean package"
}

stage('sonarqubereport'){
sh "${mavenhome}/bin/mvn clean sonar:sonar"
}

stage('uploadsrtiactsintonexs'){
sh "${mavenhome}/bin/mvn clean deploy"
}
stage('Deply'){
sshagent(['62d13728-6356-44db-a2bf-a2f81154df96']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.8.135:/opt/tomcat9/webapps"
}
}


}
