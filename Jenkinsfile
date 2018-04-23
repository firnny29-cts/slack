import groovy.json.JsonOutput

def slackNotificationChannel = 'general'     // ex: = "builds"

def notifySlack(text, channel, text1) {
    def slackURL = 'https://hooks.slack.com/services/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'
    def jenkinsIcon = 'https://wiki.jenkins-ci.org/download/attachments/2916393/logo.png'

    def payload = JsonOutput.toJson([text: text,
        channel: channel,
        username: "Jenkins",
        icon_url: jenkinsIcon,
        text1: text,
        ])

    sh "curl -X POST --data-urlencode \'payload=${payload}\' ${slackURL}"
}

node {
    stage("Post to Slack") {
        notifySlack(BUILD_URL, slackNotificationChannel, "Status")
    }
node {
    stage("Post to Slack") {
        notifySlack(BUILD_URLconsole, slackNotificationChannel, "Status")
    }
}
