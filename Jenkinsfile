node ('App-Server-CWEB2140') 
{  
    def app
    stage('CLONE GIT REPOSITORY') {
        /* Let's make sure we have the repository cloned to our workspace */
       checkout scm
    }  

    stage('SCA-SAST-SNYK-TEST') {
        snykSecurity(
            snykInstallation: 'Snyk',
            snykTokenId: 'Synkid',
            severity: 'critical'
        )
        
    }

     stage('SonarQube Analysis') 
     {
      def scannerHome = tool 'SonarQubeScanner';
      withSonarQubeEnv('sonarqube')
      {
      sh "${scannerHome}/bin/sonar-scanner -X \
          scannerHome.projectKey=Snake_Game"
      }
                    
     }
   
    stage('BUILD-AND-TAG') {
        /* This builds the actual image; 
         * This is synonymous to docker build on the command line */
        app = docker.build("amalan06/snake_game_2024")
    }

    stage('POST-TO-DOCKERHUB') {    
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
            app.push("latest")
        }
    }
    
    stage('DEPLOYMENT') {    
        sh "docker-compose down"
        sh "docker-compose up -d"	
    }
}
