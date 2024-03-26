node ('Sonarqube-Server-CWEB2140') 
{  
    
    
     stage('SonarQube Analysis') 
     {
      def scannerHome = tool 'SonarQubeScanner';
      withSonarQubeEnv('sonarqube')
      {
      sh "${scannerHome}/bin/sonar-scanner -X"
      }
                    
     }
   
  
}
    
   
