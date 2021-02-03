pipeline 
{
    agent any
    environment
    {
        PATH ="C:/Program Files/Apache Software Foundation - Maven/apache-maven-3.6.3/bin:$PATH"
    }
    tools 
    {
        maven 'LocalMaven'
    }
    
    stages 
    {
        stage("Build") 
        {
            steps 
            {
           
                git 'https://github.com/Said33pika/mavenApp-hello-world.git'
                bat 'mvn clean package'
                echo 'hello'
                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                //bat "mvn -Dmaven.test.failure.ignore=true clean package"

            }
            /*when 
            {
                branch 'master'
            }*/
            //steps { echo 'Senpai xD' }
        }
            
        stage("Test") 
        {
            parallel
            {
                stage("Unit Test")
                {
                    steps { echo 'Runnning the unit test' }
                }
                stage("Integration Test")
                {
                    steps { echo 'Running the integration test' }
                }
            }
            /*steps 
            { 
                //sh 'mvn test' 
                input ('Do you want to proceed?')
                
            }*/
        }
        
        stage("Deploy") 
        {
            steps 
            {
                echo 'Deploying the build..'
                bat 'mvn deploy'
                //sh 'mvn deploy'
            }
        }

    }
}
