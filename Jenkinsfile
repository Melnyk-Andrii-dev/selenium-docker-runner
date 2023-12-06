pipeline{

    agent any

    parameters {
        choice choices: ['chrome', 'firefox'], description: 'Select the browser', name: 'BROWSER'
    }


    stages{
        stage("Start Grid"){
            steps{
                bat "docker-compose -f grid.yaml up --scale ${params.BROWSER}=1 -d"
            }
        }
        stage("Run Test"){
            steps{
                bat "docker-compose -f test-suites.yaml up"
            }
        }
    }
    post{
        always{
            bat "docker-compose -f grid.yaml down"
            bat "docker-compose -f test-suites.yaml down"
            archiveArtifacts artifacts: 'C:\\workspace\\06-jenkins-ci-cd\\11-runner-approach-2\\output\\flight-reservation\\emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'C:\\workspace\\06-jenkins-ci-cd\\11-runner-approach-2\\output\\vendor-portal\\emailable-report.html', followSymlinks: false
        }
    }
}