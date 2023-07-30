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
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Gopi0527/spring-petclinic.git',
                    branch: 'develop'
            }
        }
        stage('build and package') {
           rtMavenDeployer (
                    id: "SPC_DEPLOYER",
                    serverId: "JFROG",
                    releaseRepo: diviseema-libs-release-local,
                    snapshotRepo: diviseema-libs-snapshot-local
                )

               stage ('Exec Maven') {
                    steps {
                        rtMavenRun (
                            tool: MAVEN, // Tool name from Jenkins configuration
                            pom: 'maven-examples/maven-example/pom.xml',
                            goals: 'clean install',
                            deployerId: diviseema-libs-release-local,
                            snapshotRepo: diviseema-libs-snapshot-local
                        )
                    }
            }
                stage ('Publish build info') {
                steps {
                    rtPublishBuildInfo (
                        serverId: "JFROG"
                    )
                }
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
