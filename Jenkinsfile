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
        notifySlack(currentBuild.getPreviousBuild().result, slackNotificationChannel, "Status")
    }
}
post {
        always  {
            echo "Build completed. currentBuild.result = ${currentBuild.result}"
        }

        changed {
            echo 'Build result changed'

            script {
                if(currentBuild.result == 'SUCCESS') {
                    echo 'Build has changed to SUCCESS status'
                }
            }
        }

        failure {
            echo 'Build failed'
        }

        success {
            echo 'Build was a success'
        }
        unstable {
            echo 'Build has gone unstable'
        }
    }
