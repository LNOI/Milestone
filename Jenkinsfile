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
            parallel{
                stage("1"){
                    steps{
                        sh 'echo "1"'
                    }
                }
                stage("2"){
                    steps{
                        sh 'echo "2"'
                    }
                }
            }
            parallel{
                stage("1"){
                    steps{
                        sh 'echo "1"'
                    }
                }
                stage("2"){
                    steps{
                        sh 'echo "2"'
                    }
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