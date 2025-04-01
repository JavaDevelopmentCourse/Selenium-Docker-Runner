pipeline{

    agent any

    stages{

        stage('Run GRID')
        {
            steps{
                bat "docker-compose -f grid.yaml up -d"
                
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