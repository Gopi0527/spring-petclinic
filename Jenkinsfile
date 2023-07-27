pipeline {
    agent { lable 'jdk-17'}
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'jdk-17'
    }
    stages{
        stage('vcs'){
            steps {
               steps {
                git branch: 'main', url: 'https://github.com/dummyrepos/spring-petclinic-1.git'
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