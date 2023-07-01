pipeline 
{
    agent any
    stages
    {
        stage('contdown')
        {
            steps{
                     git 'https://github.com/intelliqittrainings/maven.git'   
                 }
        }
        stage('contbuild')
        {
            steps{
                     sh 'mvn package'
                 }
        }
        stage('contdeploy')
        {
            steps{
                     deploy adapters: [tomcat9(credentialsId: 'd2043531-c89e-4bfc-a6d7-b4acceba90c4', path: '', url: 'http://172.31.33.155:8080')], contextPath: 'qaa', war: '**/*.war' 
                 }
                
        }
        stage('conttest')
        {
            steps{
                     git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                     sh 'java -jar /var/lib/jenkins/workspace/declarativepipeline/testing.jar'
                 }
        }
        stage('contdelivery')
        {
            steps{
                      input message: 'Please Approve the Release', submitter: 'kiranr'
                     deploy adapters: [tomcat9(credentialsId: 'd2043531-c89e-4bfc-a6d7-b4acceba90c4', path: '', url: 'http://172.31.33.155:8080')], contextPath: 'prodapp', war: '**/*.war'
                 }
        }
   
    }
    
    
}
