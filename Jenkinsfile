pipeline 
{
    agent any
    tools 
    {
        maven 'mvn'
        git 'Default'
    }

    stages 
    {
        stage('Git') 
        {
            steps 
            {
                git branch: 'main', credentialsId: '82a0c36c-66a7-4823-88c9-95551fdab537', url: 'https://github.com/fdemarais/hello_world'
            }
        }
        stage('Clean') 
        {
            steps 
            {
                bat 'mvn clean'
            }
        }
        stage('Install') 
        {
        steps 
            {
                bat 'mvn install'
            }
        }
        stage ('Quality')
        {
            parallel
            {
                stage('Tests') 
                {
                    steps 
                    {
                        bat 'mvn test'
                    }
                }
                stage('Sonar') 
                {
                    steps
                    {
                        withSonarQubeEnv('sonarqube server') 
                        {
                            bat 'mvn sonar:sonar'
                        }
                    }
                }
            }
        }
    }
    post
    {
        success
        {
            archiveArtifacts artifacts: 'target/hello_world-1.0-SNAPSHOT.jar', followSymlinks: false
            junit 'target/surefire-reports/*.xml'

        }
        failure
        {
            junit 'target/surefire-reports/*.xml'
        }
    }
}
