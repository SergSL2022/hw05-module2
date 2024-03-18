pipeline {
    agent { label "netx"}

    stages {
        stage('Checkout') {
            steps{
                echo "Pull code from github repository"
                sh """
                    pwd
                    ls -la
                """
                git branch: 'main',
                    credentialsId: 'github',
                    url: 'git@github.com:SergSL2022/hw05-module2.git'
                sh "ls -la"
            }
        }

        stage('Build') {
            steps{
                echo "create folder and file with current data and time named pipeline/BUILD_NUMBER.txt"
                sh """
                    pwd
                    ls -la
                    if [ ! -d "pipeline" ]; then
                        mkdir pipeline
                    fi
                    echo \"Current date and time: \$(date)\" > pipeline/${BUILD_NUMBER}.txt
                    ls -la
                    cd pipeline
                    pwd
                    ls -la
                """
            }
        }

        stage('Publish') {
            steps {
                echo "Adding the file to git, committing change, adding tag pushing to origin"
                sh """
                git config --global user.email "ZGravity@ukr.net"
                git config --global user.name "SergSL2022"
                git status
                git add .
                git commit -m "Add file ${BUILD_NUMBER}.txt"
                git tag -a v0.2.${BUILD_NUMBER} -m "my version 0.2.${BUILD_NUMBER}"
                git push --set-upstream origin main --follow-tags
                """
            }
        }

        stage('Post Build') {
            steps {
                sh "pwd"
                sh "ls -la"
                archiveArtifacts artifacts: "pipeline/${BUILD_NUMBER}.txt", onlyIfSuccessful: true
            }
        }

    }
}