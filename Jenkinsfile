pipeline{
    agent any
    environment{
        PATH="$PATH"
    }
    stages{
        stage("Init"){
            steps{
                script{
                    echo "Script begin for pipline"
                }
            }
        }
        stage("Init2"){
            steps{
                script{
                    echo "Print PATH=$PATH"
                }
            }
        }
        stage("Test static code"){
            steps{
                script{
                    echo "pull code "
                }
               
            }
            steps{
                script{
                    echo "scan code"
                }
            }
        }
        stage("Deploy"){
            steps{
                script{
                    echo "Deploy"
                }
            }
        }

    }



}