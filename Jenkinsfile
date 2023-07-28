pipeline 
{
    agent any
    tools 
    {
        maven 'mvn'
    }

    stages 
    {
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
        stage('Tests') 
        {
            steps 
            {
                bat 'mvn test'
            }
        }
        stage('Sonar') 
        {
            environment 
            {
                def scannerHome = tool 'scan';
            }
            steps 
            {
                bat "\"${scannerHome}\\bin\\sonar-scanner.bat\" -Dsonar.token=sqa_617e409f7f5cc520ed7d9ae18f62a1864ad6d9e0 -Dsonar.projectKey=hello_world -Dsonar.java.binaries=target"
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
