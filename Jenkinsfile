pipeline{
    agent any
    tools{
        maven 'Maven_HOME'
    }
    stages{
        stage('Checkout SCM'){
            steps{
                git url: 'https://gitlab.com/123Balu42/Jenkins_Spring.git'
            }
        }
        
        stage('Build'){
            steps{
                echo "Running Job: ${env.JOB_NAME}\n build: ${env.BUILD_ID}"
                sh 'mvn -f ./pom.xml clean install package'
            }

        }
    }
}
