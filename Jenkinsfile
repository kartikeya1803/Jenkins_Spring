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
            post{
                success{
                    archiveArtifacts(artifacts: 'Jenkins_Spring/target/*.war, allowEmptyArchive: true)
                }
            }

        }
        stage('Deploy'){
            steps{
                sh 'cp /var/jenkins_home/workspace/DemoStream_Pipeline/springmvc-maven/target/spring-mvc-maven.war /opt/tomcat/webapps'
            }
        }
        post{
            failure{
                mail to: '123balu42@gmail.com' from: '123balu42@gmail.com'
                Subject: "Project Build: ${env.JOB_NAME} - Failed"
                body: "Job Failed - \ "${env.JOB_NAME}\" build: ${env.BUILD_NUMBER}

            }
            success{
                emailext attachPattern: "*target/*.war",
                body: '''${SCRIPT, template="groovy-template"}''',
                subject: "Project Build: ${env.JOB_NAME} - SUCCESS"
                mimeType: 'text/html'
                to: 123balu42@gmail.com

            }
        }
    }
}
