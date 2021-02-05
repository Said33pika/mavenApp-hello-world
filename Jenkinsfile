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
           
                git branch: 'main', url: 'https://github.com/Said33pika/mavenApp-hello-world.git'
                /*checkout([$class: 'GitSCM',
                branches: [[name: 'main']],
                doGenerateSubmoduleConfigurations: false,
                extensions: [[$class: 'CloneOption', timeout: 120, depth: 2, noTags: false, reference: '', shallow: true], [$class: 'SubmoduleOption', recursiveSubmodules:                       false], [$class: 'CleanBeforeCheckout'], [$class: 'CleanCheckout']],
                submoduleCfg: [],
                userRemoteConfigs: [[ url: 'https://github.com/Said33pika/mavenApp-hello-world.git']]
                ])*/
                
                bat 'mvn clean package'
          
                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                //bat "mvn -Dmaven.test.failure.ignore=true clean package"

            }
            /*when 
            {
                branch 'master'  (condition to be met to exec next step, works on the whole stage)
            }*/
            
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
                    steps 
                    { 
                        echo 'Running the integration test'
                        bat 'call mvn test'
                        input ('Do you want to proceed?')
                    }
                    
                }
            }

        }
        
        stage("Deploy") 
        {
            steps 
            {
                echo 'Deploying the build..'
                //bat 'call mvn clean deploy' //why not deploying???????????????????
                
               // mvn -X -e deploy:deploy-file "-DgeneratePom=true" "-Durl=http://repo_location" -DrepositoryId=internal-repository" "-DgroupId=com.devsys" "-DartifactId=report"                     "-Dbuild.number=%BUILD_NUMBER%" "-Dpackaging=json" "-Dfile=%WORKSPACE%\backend-acceptance-tests\target\cucumber.json"
            }
        }

    }
}
