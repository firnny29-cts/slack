#!/usr/bin/env groovy

import groovy.json.JsonOutput

def slackNotificationChannel = 'general'     // ex: = "builds"
def colorName = 'RED'
def colorCode = '#FF0000'
def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
def summary = "${subject} (${env.BUILD_URL})"

def notifySlack(summary, message, attachments) {
    def slackURL = 'https://hooks.slack.com/services/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'
    def jenkinsIcon = 'https://wiki.jenkins-ci.org/download/attachments/2916393/logo.png'

    def payload = JsonOutput.toJson([text: text,
        channel: channel,
        username: "admin",
        icon_url: jenkinsIcon,
        attachments: attachments
    ])
if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESSFUL') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }
    sh "curl -X POST --data-urlencode \'payload=${payload}\' ${slackURL}"
}

node {
    stage("Post to Slack") {
        notifySlack(summary, slackNotificationChannel, [])
    }
}
