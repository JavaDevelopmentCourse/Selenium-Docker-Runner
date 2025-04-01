pipeline{

    agent any

    stages{

        stage('Run Test')
        {
            steps{
                bat "docker-compose up"
                
            }
        }
        stage('Bring GRID Down')
        {
        steps{
                
                bat "docker-compose down"
            }
        }

        
    }
}