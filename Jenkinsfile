node{
   stage('Checkout')
    {
        checkout scm
    }
	stage('Clean')
    {
		
		
			bat "mvn -f Pipeline_test/pom.xml clean"
		

    }
	 stage('Unit Test')
    {
		
		bat "mvn -f Pipeline_test/pom.xml test"
		
    }
    
   
   
    stage('Packaging')
    {
       
		bat "mvn -f Pipeline_test/pom.xml install"
		
    }
	
	
  
   
   stage('Deploy?')
    {
       input 'Proceed to Deploy?'
    }
   
   stage('Deploy')
   {
   
    
	withCredentials([usernamePassword(credentialsId: 'Web_Logic', passwordVariable: 'password', usernameVariable: 'username')]) {
		bat " mvn -f Pipeline_Test/pom.xml package -Ddeploy.to.weblogic -Ddeploy.for.weblogic"
}

}
  
	
	stage('Selenium')
	{
		bat "mvn -f SeleniumTest/pom.xml clean test"
	}
 
	
   
}

    
 
