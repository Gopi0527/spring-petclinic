pipeline{
    agent { label 'JDK-17' }
    // agent any
    // // #for multi agents 
    // // agent { label 'Label name' }
    triggers { 
        pollSCM('* * * * *') }
     tools {
        maven 'Maven-3.9' 
    }
    stages{
        stage ('VCS'){
            steps{
                git url: 'https://github.com/Gopi0527/spring-petclinic.git',
                branch: 'main'
            }
        }
        stage ( 'build' ){
            steps{
                sh 'mvn clean package'
                withSonarQubeEnv(installationName: 'SONAR_CLOUD', credentialsId: 'SONAR_CLOUD'){
                    sh 'mvn clean package sonar:sonar -Dsonar.host.url=https://sonarcloud.io -Dsonar.organization=spring-petclinic-gopi -Dsonar.projectKey=spring-petclinic-gopi_nop'
                }
            }
            post {
                success{
                    archiveArtifacts artifacts: '**/spring-petclinic-*.jar'
                    junit testResults: '**/TEST-*.xml'
                    // mail subject: 'build stage success',
                    //      from: 'build@krishna.io',
                    //      to: 'all@krishna.io',
                    //      body: "Refer to $BUILD_URL for more details"
                }
                failure{
                    mail subject: 'build stage success',
                         from: 'gopi.io',
                         to: 'gopi.io',
                         body: "Refer to $BUILD_URL for more details"
                }
            }
        }
        
    }
}