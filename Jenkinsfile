pipeline {
    agent { label 'maven' }
    stages {
        stage('Prepare') {
            steps {
                sh 'printenv'
            }
        }
        stage('Build') {
            when {
                expression { env.CHANGE_ID != null } // Pull request
            }
            steps {
                sh 'export JAVA_HOME=/usr/lib/jvm/java-11-openjdk;mvn -B -V clean verify -Prun-its -Pci'
            }
        }
        stage('Deploy') {
            when { branch 'master' }
            steps {
                echo "Deploy"
                sh 'mvn help:effective-settings -B -V clean deploy -e'
            }
        }
    }
}
