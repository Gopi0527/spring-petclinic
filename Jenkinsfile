    pipeline {
        agent { lable 'jdk-17'}
        options {
            timeout(time: 30, unit: 'MINUTES')
        }
        triggers {
            pollSCM('* * * * *')
        }
        tools {
            jdk 'JDK-17'
        }
        stages{
            stage('vcs'){
                steps {
                steps {
                    git url: 'https://github.com/Gopi0527/spring-petclinic.git',
                    branch: 'develop'
                } 
            }
            }
            stage('build and package') {
                steps {
                    sh script: 'mvn package'
                } 

            }stage('reporting') {
                steps {
                    archiveArtifacts artifacts: '**/traget/spring-petclinic-*.jar'
                    junit testResults: '**/terget/surefire-reports/TEST-*.xml'              

                } 
        }
    }
}

