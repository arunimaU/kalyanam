
pipeline{

    agent any

    stages{
     
         stage('Getting Code From GitHub')
      {
        steps {
              git 'https://github.com/arunimaU/kalyanam.git'
              }
      }

        stage('Build'){

            steps{

             sh '/opt/maven/bin/mvn clean verify sonar:sonar -Dmaven.test.skip=true'

            }

        }
        
     
        stage ('Deploy'){
            steps{
                sh '/opt/maven/bin/mvn clean deploy -Dmaven.test.skip=true'
            }
        }
        
        stage('Release'){
            steps{
                sh 'export JENKINS_NODE_COOKIE=dontkillme ;nohup java-jar $WORKSPACE/target/*.jar &'
                }
                }
                stage ('DB Migration') {
		steps {
			sh '/opt/maven/bin/mvn clean flyway:migrate'
		}
	}

    }

}
