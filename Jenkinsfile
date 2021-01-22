pipeline{
    agent any

    stages{
        stage("test"){
            steps{
                echo "compiling and packaging"
                sh 'mvn clean package'
            }
            
        }
        stage('Deploy WAR') {
            steps([$class: 'BapSshPromotionPublisherPlugin']) {
                sshPublisher(
                    continueOnError: false, failOnError: true,
                    publishers: [
                        sshPublisherDesc(
                            configName: "web1",
                            verbose: true,
                            transferSet {
                                sourceFiles('**/*.war')
                                removePrefix('target')
                            }
                            // transfers: [
                            //     sshTransfer(execCommand: "echo 'Hello World' "),
                            //     sshTransfer(removePrefix: "target"),
                            //     sshTransfer(sourceFiles: "**/*.war",),
                                
                                
                            // ]
                        )
                    ]
                )
           }
        }
    }
 
}