pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/evalight/AVSrgr.git'
        BRANCH_NAME = 'main'  
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Get Changed Files') {
            steps {
                script {
                    // Получаем список измененных файлов в последнем коммите
                    def changes = sh(script: "git diff --name-only HEAD~1 HEAD", returnStdout: true).trim()
                    if (changes) {
                        echo "Changed files: ${changes}"

                        changes.split("\n").each { file ->
                            echo "Contents of ${file}:"
                            if (fileExists(file)) {
                                sh(script: "cat ${file}")
                            } else {
                                echo "File ${file} not found in the repository."
                            }
                        }
                    } else {
                        echo "No changes detected in the last commit."
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution finished.'
        }
    }
}
