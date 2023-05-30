pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/shindevinud/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
               sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                sh 'scp /var/lib/jenkins/workspace/DeclarativePipeline1@2/webapp/target/webapp.war ubuntu@172.31.85.69:/var/lib/tomcat9/webapps/testapp.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
             git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
               input message: 'waiting for approval from DM', submitter: 'shivansh'
               deploy adapters: [tomcat9(credentialsId: 'c1bb2902-44a6-4598-a4d3-f031e588e913', path: '', url: 'http://172.31.94.113:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
