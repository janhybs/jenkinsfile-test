// git url: 'https://github.com/janhybs/jenkinsfile-test.git

def libs = [
    'mpich': 'flow123d/base-env',
    // 'yamlcpp': 'flow123d/base-build'
]

// Required due to JENKINS-27421
@NonCPS
List<List<?>> mapToList(Map map) {
  return map.collect { it ->
    [it.key, it.value]
  }
}

pipeline {
    agent { node { label 'ci2runner' } }

    stages {
        stage('Build DEBUG libs') {
            steps {
              dir('cmakefiles') {
                  script {
                      for (lib in mapToList(libs)) {
                            sh "make IMAGE=${lib[1]} BUILD_TYPE=Debug ${lib[0]}"
                        }
                    }
                }
            }
        }

        stage('Build RELEASE libs') {
            steps {
              dir('cmakefiles') {
                  script {
                      for (lib in mapToList(libs)) {
                            sh "make IMAGE=${lib[1]} BUILD_TYPE=Release ${lib[0]}"
                        }
                    }
                }
            }
        }
    }
}
