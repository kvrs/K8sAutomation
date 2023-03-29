import groovy.json.JsonSlurper
import groovy.json.JsonOutput
import groovyx.net.http.HTTPBuilder
import groovyx.net.http.ContentType

// JIRA API endpoint and credentials
def jiraUrl = "https://sekhar-voxs.atlassian.net/rest/api/2/"
def jiraUser = "snspmr@gmail.com"
def jiraPassword = "naidu579"

// Set up HTTPBuilder for Jenkins
def jenkinsHttp = new HTTPBuilder(jenkinsUrl)
jenkinsHttp.auth.basic(jenkinsUser, jenkinsPassword)

// Jenkins authentication check
def jenkinsResponse = jenkinsHttp.get(path: "api/json")
if (jenkinsResponse.status != 200) {
    throw new RuntimeException("Jenkins authentication failed")
}

println("Authentication successful!")
