pipeline {
    agent any

    environment {
        BUILD_DIR = 'build'
        ARTIFACT_NAME = 'app.jar'
    }

    stages {
        stage('Checkout Source') {
            steps {
                git url: 'https://github.com/gbhat618/dummy.git', branch: 'main'
            }
        }

        stage('Static Code Analysis') {
            steps {
                echo 'Running static analysis...'
                // sh 'mvn checkstyle:check'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                // sh 'mvn clean package -DskipTests'
            }
        }

        stage('Unit Tests') {
            steps {
                echo 'Running unit tests...'
                // sh 'mvn test'
            }
        }

        stage('Integration Tests') {
            steps {
                echo 'Running integration tests...'
                // sh 'mvn verify -Pintegration-tests'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scans...'
                // sh 'mvn dependency-check:check'
            }
        }

        stage('Package Artifact') {
            steps {
                echo 'Packaging artifact...'
                // sh "cp target/${ARTIFACT_NAME} ${BUILD_DIR}/"
            }
        }

        stage('Deploy to Staging') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying to staging...'
                // sh './deploy.sh --env=staging'
            }
        }

        stage('Approval for Production') {
            when {
                branch 'main'
            }
            steps {
                script {
                    input message: 'Approve deployment to production?'
                }
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying to production...'
                // sh './deploy.sh --env=production'
            }
        }
    }

    post {
        success {
            echo 'Build and deployment succeeded!'
            // mail to: 'team@example.com',
            //      subject: 'Jenkins Build Success',
            //      body: 'The build and deployment completed successfully.'
        }
        failure {
            echo 'Build or deployment failed!'
            // mail to: 'team@example.com',
            //      subject: 'Jenkins Build Failed',
            //      body: 'The build failed. Please check Jenkins logs for details.'
        }
    }
}
