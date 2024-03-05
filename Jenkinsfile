node ('App-Server-CWEB2140') 
{  
    def app
    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */
       checkout scm
    }  

    stage('Sny Security Test') {
        snykSecurity(
            snyKInstallation: 'Snyk',
            snykTokenId: 'Synkid',
            severity: 'high'
        )
        
    }
   
    stage('Build-and-Tag') {
        /* This builds the actual image; 
         * This is synonymous to docker build on the command line */
        app = docker.build("amalan06/snake_game_2024")
    }

    stage('Post-to-dockerhub') {    
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
            app.push("latest")
        }
    }
    
    stage('Pull-image-server') {    
        sh "docker-compose down"
        sh "docker-compose up -d"	
    }
}
