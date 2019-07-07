pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/prakashk0301/maven-project'
        }
  }
    {
        stage ('Compile Stage') {
            agent { label 'maven'}
        
            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn install'
                }
            }
        }
        
        stage ('Deploy Stage') {

            steps {
               
    sshagent (credentials: ['d9846ee0-82c8-4c43-95a8-e1e51562a6ea']) {
    sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@18.191.224.83:/var/lib/tomcat/webapps'
  }
}
       
}
}
}


