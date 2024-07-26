pipeline {
    agent {
        node {
            label 'AGENT1'
        }
    }
    environment {
        packageVersion = ''
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
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
        
    }
//POST BUILD
    post {
        always {
            echo 'I will always say hello again'
        }
        failure {
            echo 'this runs when pipeline is failed, used generally to send some alerts'
        }
        success {
            echo 'I will say hello when pipeline is success'
        }
    }
}