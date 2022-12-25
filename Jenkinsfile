#!/usr/bin/env groovy
pipeline {
  agent any
  
  options {
    buildDiscarder(logRotator(numToKeepStr: '3', artifactNumToKeepStr: '3'))
  }

  environment {
    WEBHOOK = credentials('discord_webhook')
  }

  stages {
    stage("Build") {
      steps {
        echo "Build!"
      }
    }

    stage("Testing") {
      parallel {
        stage("Unit Tests") {
            steps {
                echo "Unit Tests!"
            }
        }
        stage("Functional Tests") {
            steps {
                echo "Functional Tests!"
            }
        }
        stage("Integration Tests") {
          steps {
            echo "Integration Tests!"
          }
        }
      }
    }

    stage("Deploy") {
      steps {
        echo "Deploy!"
      }
    }
  }

  post {
    always {
      echo "Sending Discord Notification"
      discordSend title: "Parallel Pipeline", description: "Jenkins Pipeline Build #$env.BUILD_NUMBER", footer: "Footer Text", link: env.BUILD_URL, result: currentBuild.currentResult, webhookURL: WEBHOOK
    }
  }
}