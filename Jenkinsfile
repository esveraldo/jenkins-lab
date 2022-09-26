pipeline {
    // agent any
    agent { label 'jenkins-ecs-build' }

    stages {

        stage('Privisioning Slave') {
            steps {
                echo 'Done...'
            }
        }

        // Build General Dependencies
        stage('Dependencies') {
            steps {
                sh "apt-get install -y"
                sh "curl -sL https://deb.nodesource.com/setup_8.x | bash -"
                sh "apt-get install -y nodejs"
            }
        }

        //  Build package and install vendor packages
        stage('Build') {
            steps {
                echo 'Building..'
                sh "https://github.com/esveraldo/jenkins-lab.git"
                dir("micro-api/") {
                    sh "pwd"
                    sh "npm install"
                    sh "ls -lha"
                }
            }
        }

        stage('Linter') {
            steps {
                dir("micro-api/") {
                    echo 'Fake linter...'
                }
            }
        }

        // Run unit tests
        stage('Unit Tests') {
            steps {
                dir("micro-api/") {
                    sh "ls -lha"
                    echo 'Testing..'
                    sh "npm run unit-test"
                }
            }
        }
      
        // Deploy
        stage('Deploy') {
            steps {
                echo 'Fake Deploy'
            }
        }
    }

    post {
        always {
            // Clean Workspace
            cleanWs()
        }
    }
}
