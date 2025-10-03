pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/sanazbahmankhahios/CICDDemo.git'
            }
        }

        stage('Lint') {
            steps {
                sh '''
                    set -e
                    echo "Running SwiftLint..."
                    mint run realm/SwiftLint@0.61.0 lint --strict --config .swiftlint-ci.yml --reporter xcode
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                    xcodebuild \
                        -workspace CICD.xcworkspace \
                        -scheme CICD \
                        -sdk iphonesimulator \
                        -destination 'platform=iOS Simulator,name=iPhone 16 Pro,OS=18.0' \
                        clean build
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    xcodebuild \
                        -workspace CICD.xcworkspace \
                        -scheme CICD \
                        -sdk iphonesimulator \
                        -destination 'platform=iOS Simulator,name=iPhone 16 Pro,OS=18.0' \
                        test
                '''
            }
        }
    }
}
