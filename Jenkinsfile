pipeline {
    agent any

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }   
        stage('Docker Build') {
            steps {
                powershell (script: 'docker images -a')
                powershell (script:"""
                    cd C:\Users\mahmood.haq\OneDrive - Rogers Communications Inc\Mahmood\repository\MyRepo\azure-voting-app-redis\azure-vote\
                    docker images -a
                    docker build -t jenkins-pipeline .
                    docker images -a
                    cd ..
                    """)
            }
        }       
    }
}
