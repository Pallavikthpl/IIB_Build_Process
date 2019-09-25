pipeline {
    agent any
	environment
	{
	ant_build = "https://github.com/Pallavikthpl/IIB_Build_Process/tree/master/HttpReqReply/Build/build.xml"
	}
    stages {
	    
        stage('Build') { 
            
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Pallavikthpl/IIB_Build_Process.git']]])
            }
        }
        
        stage('Sonarqube') {
		environment {
        scannerHome = tool 'LocalSonarQubeScanner'
		}
		steps {
        withSonarQubeEnv('sonar_server') {
            bat "${scannerHome}/bin/sonar-scanner"
        }
		}
		}
	  stage('Build') {
		steps
		{
		withAnt(installation: 'Ant 1.10.7', jdk: 'jdk-11.0.4') {
		// some block
		bat "ant -f ${ant_build}"
		}
		}
	}
        stage('Deploy') {
                
            steps {
                bat "echo Deploy"
            }
        }
    }
}
