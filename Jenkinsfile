env.Summary = env.Summary
env.Description = env.Description
env.Story_points = env.Story_points
env.Issuetype = env.Issuetype
env.Assignee = env.Assignee
env.Labels = env.Labels
env.email_id = 'snspmr@gmail.com'

node("mynode")
{
    wrap([$class: 'BuildUser'])
    {
        env.user = env.BUILD_USER_ID
        env.first_name = env.BUILD_USER_FIRST_NAME
        env.last_name = env.BUILD_USER_LAST_NAME
        env.name = first_name+"_"+last_name
        env.user_id = env.BUILD_USER_ID

        stage("Triggering Jira Ticket & Email Notification & Usage Statistics")
        {
            jiraemail(first_name,last_name,email_id,user_id)
        }
    }
}

void jiraemail(first_name,last_name,email_id)
{
    def details = 'details of Jira'
    println(user_id)
    println(Description)
    def CreateJira_Body = """ {
        "fields": {
                    "project": {"key": "UKSAS"},
                    "summary": "${Summary}",
                    "description": "${Description}",
                    "issuetype": {"name": "Task"},
                    "assignee": {"name": "GB-UKSAS"},
                    "labels": ["AUTOMATION"]
                    }
        
        }"""
        println(CreateJira_Body)
        reponse = httpRequest authentication: 'GB-UKSAS', httpMode: 'POST',
        requestBody: CreateJira_Body,
        outputFile: 'JIRACreateOutput',
        contentType: 'APPLICATION_JSON',
        reponseHandle: 'NONE',
        url: 'https://sekhar-voxs.atlassian.net/jira/rest/api/2/issue',
        ValidResponseCodes: '100:201',
        consoleLogResponseBody: true
        println("Status: "+response.getStatus())
        if(response.getStatus() < 400)
        {
            def AppJSON = readJSON text: (response.getContent())
            def JobObj = readJSON text: (response.getContent())
            IssueID = JobObj.key
            println IssueID
            AddComments()
            UpdateJiraStatus()
            Sucessemail(IssueID)
        }
        else
        {
            def msg = "failed to create issue"
            failemail(msg)
            error(msg)
        }
    }

    def AddComments()
    {
        def JiraBrowerUrl = "https://sekhar-voxs.atlassian.net/jira/rest/api/2/issue/${IssueID}"
        def JiraCommentUrl = JiraBrowerUrl + "/comment"
        jiracommentMessage = "Comments"

        def content = "{\"body\": \"" + jiracommentMessage + "\"}"
        reponse = httpRequest authentication: 'GB-UKSAS',
        httpMode: 'POST', contentType: 'APPLICATION_JSON',
        responseHandle: 'NONE',
        outputFile: 'JIRAAddCommentOutput',
        requestBody: content, url: JiraCommentUrl,
        acceptType: 'APPLICATION_JSON',
        ignoreSslError: true
        println("Status:" +response.getStatus())
        println("exiting AddComments")
    }


// import groovy.json.JsonSlurper
// import groovy.json.JsonOutput
// import groovyx.net.http.HTTPBuilder
// import groovyx.net.http.ContentType

// // JIRA API endpoint and credentials
// def jiraUrl = "https://sekhar-voxs.atlassian.net/rest/api/2/"
// def jiraUser = "snspmr@gmail.com"
// def jiraPassword = "naidu579"

// // Set up HTTPBuilder for Jenkins
// def jenkinsHttp = new HTTPBuilder(jenkinsUrl)
// jenkinsHttp.auth.basic(jenkinsUser, jenkinsPassword)

// // Jenkins authentication check
// def jenkinsResponse = jenkinsHttp.get(path: "api/json")
// if (jenkinsResponse.status != 200) {
//     throw new RuntimeException("Jenkins authentication failed")
// }
// println("Authentication successful!")
