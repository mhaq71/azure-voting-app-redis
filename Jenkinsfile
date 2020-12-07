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
                    cd azure-vote/
                    docker images -a
                    docker build -t jenkins-pipeline .
                    docker images -a
                    cd ..
                    """)
            }
        }
        stage ('Start test app'){
            steps {
                powershell (script:"""
                docker-compose up -d
                ./script/test_container.psl
                """)        
            }
            post {
                success {
                    echo 'app started successfully :)'
                }
                failure {
                    echo 'app failed to start :('
                }
            }
        }
        stage ('Run tests') {
            steps {
                powershell (script: """
                pytest ./tests/test_sample.py
                """)        
            }                       
        }
        stage ('Stop test apply') {
            steps {
                powershell (script: """
                docker-compose down
                """)
            }
        }
    }
}
