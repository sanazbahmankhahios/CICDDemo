pipeline {
    agent any

    stages {
        //  Checkout the repository
        stage('Checkout') {
            steps {
                git url: 'https://github.com/sanazbahmankhahios/CICDDemo.git'
            }
        }

        //  Lint stage using Mint-installed SwiftLint
        stage('Lint') {
            steps {
                sh '''
                    if [ -x "./mint/bin/swiftlint" ]; then
                        echo "Running SwiftLint..."
                        ./mint/bin/swiftlint lint --strict --reporter xcode
                    else
                        echo "SwiftLint not found, failing pipeline"
                        exit 1
                    fi
                '''
            }
        }

        //  Build stage
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

        //  Test stage
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
