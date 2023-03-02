node {
    stage ("Checkout AuthService"){
        git branch: 'main', url: ' https://github.com/bgoggins/Team4ProjectAuth.git'
    }
    
    stage ("Gradle Build - AuthService") {
        sh 'gradle clean build'
    }
    
    stage ("Gradle Bootjar-Package - AuthService") {
        sh 'gradle bootjar'
    }
	
    stage ("Containerize the app-docker build - AuthApi") {
        sh 'docker build --rm -t team4-auth:v1.1 .'
    }
    
    stage ("Inspect the docker image - AuthApi"){
        sh "docker images team4-auth:v1.1"
        sh "docker inspect team4-auth:v1.1"
    }
    
    stage ("Run Docker container instance - AuthApi"){
        sh "docker run -d --rm --name team4-auth -p 8081:8081 team4-auth:v1.1"
     }
    
    stage('User Acceptance Test - AuthService') {
	
	  def response= input message: 'Is this build good to go?',
	   parameters: [choice(choices: 'Yes\nNo', 
	   description: '', name: 'Pass')]
	
	  if(response=="Yes") {
	  
	    stage('Release - AuthService') {
	      sh 'docker stop team4-auth'
	      sh 'echo Team4 MCC AuthService is ready to release!'
	    }
	  }
    }
}
