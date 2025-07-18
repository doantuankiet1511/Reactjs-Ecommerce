pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/doantuankiet1511/Reactjs-Ecommerce.git'
            }
        }

        stage('Clear workspace') {
            steps {
                sh 'rm -rf ${WORKSPACE}/fukiweb/build'
            }
        }

        stage('Build') {
            steps {
                dir('fukiweb') {
                    sh 'node --version'
                    sh 'yarn --version'
                    sh 'yarn install'
                    sh 'CI="" yarn build'
                }
            }
        }

        stage('Upload Artifacts') {
            steps {
                sh 'aws s3 cp ${WORKSPACE}/fukiweb/build/ s3://project-ecommerce-doantuankiet/ --recursive'
            }
        }

        stage('Clear CloudFront Cache') {
            steps {
                sh 'aws cloudfront create-invalidation --distribution-id E2TK2QOH8C0A2C --paths "/index.html"'
            }
        }
    }
}
