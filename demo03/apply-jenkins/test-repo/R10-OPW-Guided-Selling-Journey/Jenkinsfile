pipeline {
    agent { label 'jenkins-ubuntu-slave' }
    stages {
        stage('sonarqube'){
            steps {
                script {
                    def pipelineConfig=[
                        sonarQubeServer: 'sonarqube',
                    ]
                    def repositoryUrl = scm.userRemoteConfigs[0].getUrl()
                    def GIT_REPO_NAME = scm.userRemoteConfigs[0].getUrl().tokenize('/').last().split("\\.")[0]
                    def scannerHome = tool 'sonar_scanner'
                    def SONAR_BRANCH_NAME = env.BRANCH_NAME
                    withSonarQubeEnv(pipelineConfig.sonarQubeServer) {
                        sh "sed -i s#{{repo_name}}#${GIT_REPO_NAME}# sonar-project.properties"
                        sh "sed -i s#{{branch_name}}#${SONAR_BRANCH_NAME}# sonar-project.properties"
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectVersion=${SONAR_BRANCH_NAME} -Dsonar.buildString=Jenkins-${SONAR_BRANCH_NAME}-BLD${env.BUILD_NUMBER}"
                    }
                    //TODO: enable step (requires webhook on Sonarqube server)
                    //timeout(time: 10, unit: 'MINUTES') {
                        // waitForQualityGate abortPipeline: true
                    //} 
                }
            }
        }
    }
}