pipeline{
   agent any
   stages{
      stage('login server'){
         steps{
            sshagent(credentials:['newsshkey']){
               sh 'ssh  -o StrictHostKeyChecking=no -l cloud_user 3.101.30.226 uptime "whoami"'
//                sh 'git@github.com:kvrs/K8sAutomation.git cloud_user@54.183.168.67:${WORKSPACE}'
//                sh 'scp ${WORKSPACE}  -o StrictHostKeyChecking=no cloud_user@3.101.30.226:/test'
          }
        echo "success lgoin"
         }
       }
   }
}

// pipeline {
//     agent any
//     stages {
//         stage('Build') {
//             steps {
//               checkout([$class: 'GitSCM', 
//                 branches: [[name: '*/main']],
//                 doGenerateSubmoduleConfigurations: false,
//                 extensions: [[$class: 'CleanCheckout']],
//                 submoduleCfg: [], 
//                 userRemoteConfigs: [[url: 'https://github.com/kvrs/K8sAutomation.git']]])
//               sh "ls -ltr"
//           }
//         }
//     }
// }
   
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
