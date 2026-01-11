pipeline{
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '15'))
        disableConcurrentBuilds()
        retry(2)
        timeout(time: 5, unit: 'MINUTES')
    }
    parameters {
        string(name: 'BRANCH', defaultValue: 'main', description: 'branch to build')
        choice(name: 'ENV', choices: ['dev', 'qa', 'uat'], description: 'env to build')
    }


    stages{
        stage("Docker Login"){
            steps{
                sh '''
                docker login -u sonalisnehi -p Sona@1234
                '''
            }
        }
        
        stage("Build image"){

            steps{
                sh '''
                cd vote
                docker build -t sonalisnehi/voterepo:votetag1 .
                '''
            }
        }

        stage("Image push on Docker"){
            steps{
                sh "docker push sonalisnehi/voterepo:votetag1"
            }
        }

        stage("Docker run"){
            steps{
                sh "docker run -itd -p 81:80 sonalisnehi/voterepo:votetag1"
            }
        }

        stage("deploy"){
            steps{
                sh '''
                echo deployment success hurrey
                '''
            }
        }


        }
        }
    
