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
                    // Sửa dòng build để CI='' nhằm bỏ qua lỗi warning trong build
                    sh 'CI="" yarn build'
                }
            }
        }
        stage('Upload Artifacts') {
            steps {
                // Upload the artifact to S3
                sh 'aws s3 cp ${WORKSPACE}/fukiweb/build/ s3://project-ecommerce-doantuankiet/ --recursive'
            }
        }
    }
}