import groovy.json.JsonOutput

def slackNotificationChannel = 'general'     // ex: = "builds"
def call(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus = buildStatus ?: 'SUCCESS'
def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
def summary = "${subject} (${env.BUILD_URL})"
}
def notifySlack(text, channel, summary) {
    def slackURL = 'https://hooks.slack.com/services/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'
    def jenkinsIcon = 'https://wiki.jenkins-ci.org/download/attachments/2916393/logo.png'

    def payload = JsonOutput.toJson([text: text,
        
	channel: channel,
        username: "Jenkins",
        icon_url: jenkinsIcon,
        summary: summary,
        ])
	

    sh "curl -X POST --data-urlencode \'payload=${payload}\' ${slackURL}"
}


node {
    stage("Post to Slack") {
        notifySlack("Success", slackNotificationChannel, summary)
    }
}
