pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Clone your GitHub repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/test']], userRemoteConfigs: [[url: 'https://github.com/springernature/pcm-autopilot-poc.git']]])
                }
            }
        }
        stage('Create and Checkout Test Branch') {
            steps {
                script {
                    // Ensure the "test" branch exists and create it if not
                    bat 'git fetch origin test:refs/remotes/origin/test'
                    bat 'git checkout test'
                }
            }
        }
        stage('Commit') {
            steps {
                script {
                    // Pull the latest changes from the remote "test" branch
                    bat 'git pull origin test'
                    // Modify the README.md file
                    bat 'echo "New content" >> README.md'
                    // Commit the changes
                    bat 'git add README.md'
                    bat 'git commit -m "New commit"'
                    // Push the changes to the remote "test" branch
                    bat 'git push origin test'
                }
            }
        }
    }
}
