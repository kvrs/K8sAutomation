pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
              checkout([$class: 'GitSCM', 
                branches: [[name: '*/main']],
                doGenerateSubmoduleConfigurations: false,
                extensions: [[$class: 'CleanCheckout']],
                submoduleCfg: [], 
                userRemoteConfigs: [[url: 'https://github.com/kvrs/K8sAutomation.git']]])
              sh "ls -ltr"
          }
        }
        stage('Jira creation') {
            steps {
                script {
                
                    def jsonPayload = """
                        {
                            "fields": {
                                "project": {
                                    "key": "${env.JIRA_PROJECT}"
                                },
                                "summary": "${env.JIRA_SUMMARY}",
                                "description": "${env.JIRA_DESCRIPTION}",
                                "issuetype": {
                                    "name": "${env.JIRA_ISSUE_TYPE}"
                                },
                                "reporter": {
                                    "name": "${gitCommitAuthor}"
                                },
                                "assignee": {
                                    "name": "${env.JIRA_ASSIGNEE}"
                                }
                            }
                        }
                  """
       }
