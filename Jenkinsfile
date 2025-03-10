pipeline{
    agent { label 'my-defined-label' }
    options{
        timeout(time: 1, unit: 'HOURS') 
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages{
        stage('SCM'){
            steps{
                git url:'https://github.com/sadikshai/nopCommerce.git',
                branch:'develop'
            }
        }
        stage('BUIL'){
            steps{
                 sh 'dotnet build -c Release src/Presentation/Nop.Web/Nop.Web.csproj'
                 sh 'mkdir published && dotnet publish -o ./published -c Release src/Presentation/Nop.Web/Nop.Web.csproj'
            }
            post{
                success{
                     zip zipFile: './published.zip',
                         archive: true,
                         dir: './published'

                }
            }
        }

        
    }
}