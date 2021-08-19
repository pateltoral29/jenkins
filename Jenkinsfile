pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        mvnHome = tool 'maven3.8'
        env.PATH = env.PATH + ";c:\\Windows\\System32"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/capgteam/bankapp.git'

                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                 bat(/"%MVN_HOME%\bin\mvn" -f Day1-BankApp\\pom.xml -Dmaven.test.failure.ignore clean package/)
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'Day1-BankApp/target/*.jar'
                }
            }
        }
    }
}
