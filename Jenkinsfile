// git url: 'https://github.com/janhybs/jenkinsfile-test.git

def libs = [
    'mpich',
    'yamlcpp'
]

pipeline {
    agent { node { label 'ci2runner' } }

    stages {
        stage('Build') {
            steps {
              sh 'pwd'
              sh 'ls -la'

              dir('cmakefiles') {
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
}
