pipeline{
    agent any
    stages{
        stage('Git'){
            steps{
                git url: 'git@github.com:Naresh1770/springboot-cicd-app.git
',
                    branch: 'main'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('Docker image build'){
            steps{
                sh 'docker build -t springboot-cicd:latest .'
            }
        }
        stage('Deploy'){
            steps{
                sh '''
                docker rm -f springboot-cicd || true
                docker run -d -p 8082:8080 --name springboot-cicd springboot-cicd:latest
                '''
            }
        }
    }
    post{
        success{
            echo 'CI/CD Pipeline Completed Successfully'
        }
        failure{
            echo 'Pipeline failed'
        }
    }
}
