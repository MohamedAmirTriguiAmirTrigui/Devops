pipeline {
    agent any


    stages {
        stage('Git') {
            steps {
               git branch: 'amir', url: 'https://github.com/devCyberops/SpringDataJPA-CrudRepo.git'
            }
        }
            stage('MVN Clean') {
            steps {
                sh 'mvn clean'
                  }
        }
        stage('MVN Compile'){
            steps {
                sh 'mvn compile'
            }
        }
        stage('MVN Build'){
            steps {
                sh 'mvn install'
            }
        }
        stage ('MVN SonarQube') {
		steps {
			
                sh  "mvn sonar:sonar -Dsonar.login=ee074ba54a7030fc4acf6117d9b3a5490e12febd"
	
		}
	}
              stage("nexus deploy"){
               steps{
                       sh 'mvn clean deploy -DskipTests'
                       sh'mvn clean deploy -Dmaven.test.skip=true -Dresume=false'
               }
          }
          
          stage("Test JUnit - Mockito"){
                steps {
                            sh 'mvn test'
                }
          }

    }
}
