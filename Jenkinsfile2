pipeline
{
    agent any
    stages
    {
        stage('continuousdownload')
        {
            steps
            {
              git 'https://github.com/intelliqittrainings/maven.git'  
            }
        }
        stage('continuousbuild')
        { 
            steps
            {
              sh 'mvn package'
            }
        }
        stage('continuousdeployment')
        {
            steps
            {
               deploy adapters: [tomcat9(credentialsId: 'ef90dc98-6d02-487b-8ccc-e0d914b0dbc4', path: '', url: 'http://172.31.6.89:8080')], contextPath: 'test1', war: '**/*.war'
            }
        }
        stage('continuoustesting')
        {
            steps
           {
             git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
             sh '''java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'''
           }
        }
        stage('continuousdelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'ef90dc98-6d02-487b-8ccc-e0d914b0dbc4', path: '', url: 'http://172.31.2.152:8080')], contextPath: 'prod1', war: '**/*.war'
            }
        }
    }
}
