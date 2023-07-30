pipeline {
    agent { label 'JDK-17' }
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JDK-17'
    }
     parameters { choice(name: 'GOAL',
                choices: ['package', 'install', 'clean install','clean package'], description: 'Tis is maven goal') 
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Gopi0527/spring-petclinic.git',
                    branch: 'develop'
            }
        }
        stage('build and package') {
            steps {
                 sh script: "mvn ${params.GOAL}"
            }
        }
        stage('reporting') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-*.jar'
                junit testResults: '**/target/surefire-reports/TEST-*.xml'
            }
        }
    }
    post{
            success{
                mail subject:"${JOB_NAME}:project has complete success",
                body: "your projrct is effective \n Build url is ${BUILD_URL}",
                to: 'all@ww.com'
            }
            failure {
                mail subject:"${JOB_NAME}:project has complete success",
                body: "your projrct is deffective \n Build url is ${BUILD_URL}",
                to: 'all@ww.com'
            }
        }

}
