pipeline{
    agent any
    // #for multi agents 
    // agent { label 'Label name' }
    triggers { 
        pollSCM('* * * * *') }
    stages{
        stage ('VCS'){
            steps{
                git url: 'git@github.com:Gopi0527/spring-petclinic.git',
                branch: 'main'
            }
        }
        stage ( 'build' ){
            steps{
                sh 'mvn clean package'
            }
            post {
                success{
                    archiveArtifacts archive: '**/spring-petclinic-*.jar'
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