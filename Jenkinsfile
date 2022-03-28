pipeline{
    agent any
    triggers{
        pollSCM('* * * * *')
    }
    stages{
        // Implicit checkout stage
        // stage('Checkout'){
        //     steps {
        //         git url: 'https://github.com/NiHaLOO7/jgsu-spring-petclinic.git', branch: 'main'
        //     }
        // }
        stage('Build'){
            steps {
                // Get some code from a GitHub repository
                // Run Maven on a Unix agent.
                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package" 
                bat "./mvnw clean package"
            }
        }
    }

    post{
        // If Maven was able to run the tests, even if some of the test
        // failed, record the test results and archive the jar file.
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
        }
        // Disabling Email Alert For Now
        // changed{
        //     emailext subject: "Job /'${JOB_NAME}/' {${BUILD_NUMBER}} ${currentBuild.result}",
        //     attachLog: true, 
        //     body: "Please go to the ${BUILD_URL} and verify the build", 
        //     compressLog: true, 
        //     recipientProviders: [upstreamDevelopers(), requestor()]
        // }
    }
        
    
}
