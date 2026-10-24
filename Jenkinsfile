pipeline {
agent any

tools {
    jdk 'JDK21'
    maven 'Maven3'
}

options {
    timestamps()
    disableConcurrentBuilds()
}

stages {

    stage('Checkout Source Code') {
        steps {
            echo 'Checking out the Accounts microservice source code.'
            checkout scm
        }
    }

    stage('Verify Java and Maven') {
        steps {
            bat 'java -version'
            bat 'mvn -version'
        }
    }

    stage('Build and Test') {
        steps {
            bat 'mvn -B clean verify'
        }
    }

    stage('Archive JAR Artifact') {
        steps {
            archiveArtifacts(
                artifacts: 'target/*.jar',
                fingerprint: true
            )
        }
    }
}

post {
    success {
        echo 'SUCCESS: Accounts microservice built and tested successfully.'
    }

    failure {
        echo 'FAILURE: Check the Jenkins console output for errors.'
    }

    always {
        echo 'Accounts pipeline execution completed.'
    }
}

}
