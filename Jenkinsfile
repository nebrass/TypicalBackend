node {
    stage('checkout') {
        checkout scm
    }

    // uncomment these 2 lines and edit the name 'node-4.6.0' according to what you choose in configuration
    // def nodeHome = tool name: 'node-4.6.0', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
    // env.PATH = "${nodeHome}/bin:${env.PATH}"

    stage('clean') {
        sh "./mvnw clean"
    }

    stage('backend tests') {
        try {
            sh "./mvnw test"
        } catch(err) {
            throw err
        } finally {
            step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
        }
    }

    stage('packaging') {
        sh "./mvnw package -Pprod -DskipTests"
    }
}
