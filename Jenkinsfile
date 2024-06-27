pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
              deploy adapters: [tomcat9(credentialsId: 'cb5ebcf3-9e3d-48fe-84ee-427452464e70', path: '', url: 'http://172.31.8.244:8080')], contextPath: 'testing', war: '**/*.war'  
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
            
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'cb5ebcf3-9e3d-48fe-84ee-427452464e70', path: '', url: 'http://172.31.12.241:8080')], contextPath: 'production', war: '**/*.war'
            }
        }
    }
}
