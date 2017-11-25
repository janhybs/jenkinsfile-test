def libs = [
    'mpich',
    'yamlcpp'
]

pipeline {
    agent { node { label 'ci2runner' } }

    stages {
        stage('Build') {
            steps {
              script {
                  libs.each { lib ->
                        dir("${lib}") {
                            echo "Building library '${lib}'"
                            sh 'make help'
                        }
                    }
                }
            }
        }
    }
}
