pipeline {
    agent any
    
    environment {
        JIRA_SITE = 'https://sekhar-voxs.atlassian.net'
        JIRA_CREDENTIALS = credentials('jircredentials')
        JIRA_PROJECT = 'uksas-support'
        JIRA_ISSUE_TYPE = 'Task'
        JIRA_TRANSITION = 'Done'
    }
    stages {
        stage('Create JIRA Issue') {
            steps {
                script {
                    def jiraAuth = "${env.JIRA_CREDENTIALS}".split(':')
                    def jiraJson = """{
                        "fields": {
                            "project": {
                                "key": "${env.JIRA_PROJECT}"
                            },
                            "issuetype": {
                                "name": "${env.JIRA_ISSUE_TYPE}"
                            },
                            "summary": "Example JIRA Issue",
                            "description": "This is an example JIRA issue created by Jenkins pipeline",
                            "assignee": {
                                "name": "jira_user"
                            }
                        }
                    }"""
                    def httpResponse = httpRequest authentication: jiraAuth, contentType: 'APPLICATION_JSON', httpMode: 'POST', requestBody: jiraJson, url: "${env.JIRA_SITE}/rest/api/latest/issue"
                    def issueKey = new groovy.json.JsonSlurper().parseText(httpResponse.getContent()).key
                    println "Created JIRA issue ${issueKey}"
                }
            }
        }
        stage('Update JIRA Status') {
            steps {
                script {
                    def jiraAuth = "${env.JIRA_CREDENTIALS}".split(':')
                    def httpResponse = httpRequest authentication: jiraAuth, contentType: 'APPLICATION_JSON', httpMode: 'POST', requestBody: """{"transition": {"name": "${env.JIRA_TRANSITION}"}}""", url: "${env.JIRA_SITE}/rest/api/latest/issue/${issueKey}/transitions"
                    println "Updated JIRA issue ${issueKey} status to ${env.JIRA_TRANSITION}"
                }
            }
        }
    }
}
