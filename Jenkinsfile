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
                //sh 'python --version'
                //sh "python Dict.py"
            }
        }
        
        
    }
}

