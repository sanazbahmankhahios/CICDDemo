pipeline {
    agent any
    environment {
        SWIFTLINT_PATH = '/opt/homebrew/bin/swiftlint'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/sanazbahmankhahios/CICDDemo.git'
            }
        }

        stage('Lint') {
            steps {
                script {
                    if (fileExists(env.SWIFTLINT_PATH)) {
                        sh """
                            set -e
                            ${env.SWIFTLINT_PATH} lint --strict
                        """
                    } else {
                        echo "SwiftLint not installed, skipping lint stage"
                    }
                }
            }
        }

        stage('Build') {
            steps {
                sh """
                    xcodebuild \
                        -workspace CICD.xcworkspace \
                        -scheme CICD \
                        -sdk iphonesimulator \
                        -destination 'platform=iOS Simulator,name=iPhone 16 Pro,OS=18.0' \
                        clean build
                """
            }
        }

        stage('Test') {
            steps {
                sh """
                    xcodebuild \
                        -workspace CICD.xcworkspace \
                        -scheme CICD \
                        -sdk iphonesimulator \
                        -destination 'platform=iOS Simulator,name=iPhone 16 Pro,OS=18.0' \
                        test
                """
            }
        }
    }
}

