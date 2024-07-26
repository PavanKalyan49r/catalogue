pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        packageVersion = ''
        nexusUrl = '172.31.32.95:8081'
    }
    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
    }
//     parameters {
//         string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

//         text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

//         booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

//         choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

//         password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
//     }
// // BUILD
    stages {
        stage('Get the version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version
                    echo "application version: $packageVersion"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh"""
                    npm install
                """
            }
        }
        stage('Build') {
            steps {
                sh"""
                    ls -la
                    zip -q -r catalogue.zip ".git" -x "*.zip"
                    ls -ltr
                """
            }
        }
        stage('publish artifact') {
            steps {
                nexusArtifactUploader(
                   nexusVersion: 'nexus3',
                   protocol: 'http',
                   nexusUrl: "${nexusUrl}",
                   groupId: 'com.roboshop',
                   version: "${packageVersion}",
                   repository: 'catalogue',
                   credentialsId: 'nexus-auth',
                     artifacts: [
                            [artifactId: 'catalogue',
                            classifier: '',
                            file: 'catalogue.zip',
                            type: 'zip']
                                ]
                )
            }
        }
        
    }
//POST BUILD
    post {
        always {
            echo 'I will always say hello again'
            deleteDir()
        }
        failure {
            echo 'this runs when pipeline is failed, used generally to send some alerts'
        }
        success {
            echo 'I will say hello when pipeline is success'
        }
    }
}