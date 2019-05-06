pipeline {
    agent any
    
    checkout scm
    
    //sh "ls -la"
    
    tools { 
        maven 'Maven 3.3.9' 
    }
    
    /*triggers {
    	pollSCM 0 0-5 14 * * ?
    }*/
    
    options {
        timestamps()
        ansiColor("xterm")
    }
    
    stages {
        stage ('Initialize') {
            steps {
                echo 'kfa initializing...'
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }

        stage ('Build') {
            steps {
                echo 'kfa building...'
                sh 'mvn -Dmaven.test.failure.ignore=true clean install' 
            }
            
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
        
        /*stage ('SonarQube Analysis') {
        	steps {
        	    echo 'kfa SonarQube...'
				dir("project_templates/java_project_template") {
					withSonarQubeEnv('SonarQube5.3') {
						sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
					}
				}
			}
		}*/
    }
}