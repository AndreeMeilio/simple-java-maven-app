node {
    try {
        stage("Checkout"){
            checkout scm
        }
        stage("Build"){
            docker.image("maven:3.9.0").inside("-v /root/.m2:/root/.m2"){
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage("Test"){
            docker.image("maven:3.9.0").inside("-v /root/.m2:/root/.m2"){
                sh 'mvn test'
            }
        }
    } catch (error) {
        echo "Terjadi kesalahan: ${error.message}"
        currentBuild.result = 'FAILURE'
        throw error
    }
}