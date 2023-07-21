pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    
    environment {
        PATH = "/opt/apache-maven-3.9.3/bin:$PATH"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/ashokitschool/ashokit_insta_reels_app.git'
            }
        }
        stage('Code Build') {
            steps {
                echo "----------- build started ----------"
                sh 'mvn clean package -DskipTests=true'
                echo "----------- build completed ----------"
            }
        }
        stage("test"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                 echo "----------- unit test Complted ----------"
            }
        }
        
        stage('SonarQube analysis') {
            environment{
                scannerHome = tool 'ashokit-sonarqube-scanner'
            }
			
	    steps{
		withSonarQubeEnv('ashokit-sonarqube-server') {
		   sh "${scannerHome}/bin/sonar-scanner"
		}
	    }
        }
    }
}
