pipeline
{
    agent any
    stages
    {
        stage ("Git Checkout")
        {
            steps
            {
                echo "This is Innersource checkout step"
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/AshutoshKumar26/git-github.git']]])
            }
                
        }
        stage ("Build")
        {
            steps
            {
                echo "This is python script execution step"
                sh 'python --version'
                sh "python Dict.py"
            }
        }
        stage ("Nexus Upload")
        {
            steps
            {
                echo "This is Nexus Upload step"
                //nexusArtifactUploader artifacts: [[artifactId: 'new', classifier: '', file: 'EvenOdd.py', type: 'maven2']], credentialsId: '1d110ca2-dadc-433e-8348-74067020807a', groupId: 'new', nexusUrl: 'alm.accenture.com/nexus', nexusVersion: 'nexus3', protocol: 'http', repository: 'NexusTest1_Snapshot', version: '2.0'
                sh "curl --upload-file EvenOdd.py -u ashutosh.u.kumar:sxd@1992 -v https://alm.accenture.com/nexus/repository/NexusTest1_Snapshot/new1/"
            }
        }
        stage ("Docker Pull")
        {
            steps
            {
                echo "This is pull docker image from Azure"
                sh "docker login --username 'ADOPDemoPipeline' --password '/anG6HFgxXZpHm+Yijui2nmm0G++U7K7' 'adopdemopipeline.azurecr.io'"
                sh "docker pull adopdemopipeline.azurecr.io/hello-world:v1"
                sh "docker container run adopdemopipeline.azurecr.io/hello-world:v1"
                echo "Tagging hello-wrold image"
				sh "docker image ls -a"
                sh "docker tag hello-world adopdemopipeline.azurecr.io/hello-world:v4"
                echo "Pushing the tagged image to Azure repository"
                sh "docker push adopdemopipeline.azurecr.io/hello-world:v4"
                //archiveArtifacts 'hello-world'
            }
        }
    }
}

