pipeline{

    agent any
parameters {
  choice choices: ['chrome', 'firefox'], description: 'select the browser', name: 'BROWSER'
  choice choices: ['*.xml', 'flight-reservation.xml', 'vendor-portal.xml'], description: 'select the browser', name: 'TESTSUITES'
}


    stages{

        stage('Run GRID')
        {
            steps{
                bat "docker-compose -f grid.yaml --scale ${params.BROWSER}=2 -e ${params.TESTSUITES} up -d"
                
            }
        }
        stage('Run tests')
        {
        steps{
                
                bat "docker-compose -f test-suites.yaml up"
            }
        }



        
    }

    post{
        always{
            bat "docker-compose -f grid.yaml down"
            bat "docker-compose -f test-suites.yaml down"
             archiveArtifacts artifacts: 'ExecutionResults/Results/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'ExecutionResults/Results/vendor-portal/emailable-report.html', followSymlinks: false
        }
    }
}