node {
    docker.image('maven:3.9.0-eclipse-temurin-11').inside('-v /root/.m2:/root/.m2') {
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            try {
                sh 'mvn test'
            } finally {
                junit 'target/surefire-reports/*.xml'
            }
        }
        stage('Manual Approval') {
            input(message: 'Lanjutkan ke tahap Deploy?')
        }
        stage('Deliver') {
            sh './jenkins/scripts/deliver.sh'
            sleep(time: 60)
        }
    }
}
