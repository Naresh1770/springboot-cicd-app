pipeline{
    agent any
    stages{
        stage('Git'){
            steps{
                git url: 'https://github.com/Naresh1770/springboot-cicd-app.git',
                    branch: 'main'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('Docker image build'){
            steps{
                sh 'docker build -t naresh1770/springboot-cicd:latest .'
            }
        }
        stage('Docker push'){
             steps{
                sh ''' 
                   docker login -u naresh1770 -p Naresh@1770
                   docker push naresh1770/springboot-cicd:latest
                   '''
            }
        }
        stage('Deploy'){
            steps{
                sh '''
                docker rm -f springboot-cicd || true
                docker run -d -p 8082:8080 --name springboot-cicd naresh1770/springboot-cicd:latest
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
