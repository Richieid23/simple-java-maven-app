pipeline {
    agent {
        docker {
            image 'maven:3.9.0'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy? klik Proceed (melanjutkan eksekusi pipeline ke tahap Deploy) atau Abort (menghentikan eksekusi pipeline)'
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                sh 'sleep 1m'
            }
        }
    }
}