pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                echo 'Hello World' // this is not an sh commande it is implemented by jenkins
                sh 'echo "Hello World made by script shell"' // this is how you lunch a shell commande
                sh 'whoami' // shell commande that define the current user
            }
        }
    }
}
