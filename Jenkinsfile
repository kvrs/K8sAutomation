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
        stage('jira_creation') {
            steps {
                script{
                  def jenkins = jenkins.model.Jenkins.instance
                  for (n in jenkins.nodes) {
                  try {
                    println("${n.nodeName}")
                  } catch (Exception e) {
                  println("Exception: ${e}")
                  }
                }
            }
        }
    }
}
   
//         stage('Jira creation') {
//             steps {
//                 script {
                
//                     def jsonPayload = """
//                         {
//                             "fields": {
//                                 "project": {
//                                     "key": "${env.JIRA_PROJECT}"
//                                 },
//                                 "summary": "${env.JIRA_SUMMARY}",
//                                 "description": "${env.JIRA_DESCRIPTION}",
//                                 "issuetype": {
//                                     "name": "${env.JIRA_ISSUE_TYPE}"
//                                 },
//                                 "reporter": {
//                                     "name": "${gitCommitAuthor}"
//                                 },
//                                 "assignee": {
//                                     "name": "${env.JIRA_ASSIGNEE}"
//                                 }
//                             }
//                         }
//                   """
//        }
