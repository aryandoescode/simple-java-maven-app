pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
stage('Checkout'){
steps{
 // Get some code from a GitHub repository
                git 'https://github.com/aryandoescode/simple-java-maven-app.git'
}
}
        stage('Build') {
            steps {
               

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
 stage ('Deploy') {

        steps {
            echo "deploy stage"
            deploy adapters: [tomcat9 (
                    credentialsId: '70edc42a-6eca-47ac-b2f6-ae90834aaab8',
                    path: '',
                    url: 'http://52.170.202.98:8080/'
                )],
                contextPath: 'test',
                onFailure: 'false',
                war: '**/*.war'
        }
    }

    }
}
