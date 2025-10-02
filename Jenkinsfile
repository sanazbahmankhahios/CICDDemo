pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps { git url: 'https://github.com/sanazbahmankhahios/CICDDemo.git' }
        }
        stage('Lint'){
     steps {
                script {
                    if (fileExists(env.SWIFTLINT_PATH)) {
                        sh "${env.SWIFTLINT_PATH} lint --strict"
                    } else {
                        echo "SwiftLint not installed, skipping lint stage"
                    }
                }
            }
        }
        stage('Build') {
            steps {
                xcodebuild(
                    workspace: 'CICD.xcworkspace',
                    scheme: 'CICD',
                    sdk: 'iphonesimulator',
                    destination: 'platform=iOS Simulator,name=iPhone 16 Pro,OS=18.0'

                )
            }
        }
        stage('Test') {
            steps {
                xcodebuild(
                    workspace: 'CICD.xcworkspace',
                    scheme: 'CICD',
                    sdk: 'iphonesimulator',
                    destination: 'platform=iOS Simulator,name=iPhone 16 Pro,OS=18.0',
                    test: true
                )
            }
        }
    }
}
