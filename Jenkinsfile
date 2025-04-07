pipeline{

    agent any
parameters {
  choice choices: ['chrome', 'firefox'], description: 'select the browser', name: 'BROWSER'
}


    stages{

        stage('Run GRID')
        {
            steps{
                sh "docker-compose -f grid.yaml up --scale ${params.BROWSER}=2 -d"
                
            }
        }
        stage('Run tests')
        {
        steps{
                
                sh "docker-compose -f test-suites.yaml up --pull=always"
                script{
                    if(fileExists('ExecutionResults/Results/flight-reservation/testng-failed.xml')|| fileExists('ExecutionResults/Results/vendor-portal/testng-failed.xml'))
                    {
                        error('tests are failed please check !')
                    }
                }
            }
        }



        
    }

    post{
        always{
            sh "docker-compose -f grid.yaml down"
            sh "docker-compose -f test-suites.yaml down"
             archiveArtifacts artifacts: 'ExecutionResults/Results/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'ExecutionResults/Results/vendor-portal/emailable-report.html', followSymlinks: false
        }
    }
}