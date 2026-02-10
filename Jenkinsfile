pipeline{
    agent any
    stages{
        stage('Git'){
            steps{
                git url: 'https://github.com/jenkinsci/jenkins.git',
                    branch: 'main'
            }
        }
    }
}