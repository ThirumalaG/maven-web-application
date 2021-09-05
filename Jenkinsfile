node{
def  mavenHome = tool name: "maven3.8.1"

stage('CheckoutCode'){
git branch: 'development', credentialsId: 'c3d983e7-0af8-4af2-a730-33ec1072d2d6', url: 'https://github.com/lohithdevsolutions-ec-projects/maven-web-application.git'
}

stage('build'){
 sh "${mavenHome}/bin/mvn clean package"

}

stage('execute sonarqube report'){
 sh "${mavenHome}/bin/mvn sonar:sonar"

}
stage('upload artifacts into nexus'){
 sh "${mavenHome}/bin/mvn deploy"

}
stage(deploy app into tomcat server){
sshagent(['d97d9515-5428-4857-84a1-dabf0b0655f8']) {
    // some block
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.234.34.184:/opt/apache-tomcat-9.0.52/webapps/"
}

} 
stage('email')
{
emailext body: '''regards
lohith''', subject: 'build over', to: 'lohithkoppisetti420@gmail.com,chintusatvik007@gmail.com'
}


}
