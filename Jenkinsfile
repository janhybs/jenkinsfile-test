// git url: 'https://github.com/janhybs/jenkinsfile-test.git

// def libs = [
//     'mpich': 'flow123d/base-env',
//     'petsc': 'flow123d/base-env',
//     'yamlcpp': 'flow123d/base-env',
//     'armadillo': 'flow123d/base-env',
//     'bddcml': 'flow123d/base-env',
// ]

def debug_libs = [
    'mpich',
    // 'petsc',
    // 'yamlcpp',
    // 'armadillo',
    'bddcml',
]

def release_libs = [
    'mpich',
    'petsc',
    'yamlcpp',
    'armadillo',
    'bddcml',
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
        stage('Build DEBUG') {
            steps {
              dir('cmakefiles') {
                  script {
                      for (lib in debug_libs) {
                            sh "make IMAGE=flow123d/base-env BUILD_TYPE=Debug ${lib}"
                        }
                    }
                }
            }
        }

        stage('Build RELEASE') {
            steps {
              dir('cmakefiles') {
                  script {
                      for (lib in release_libs) {
                            sh "make IMAGE=flow123d/base-env BUILD_TYPE=Release ${lib}"
                        }
                    }
                }
            }
        }
    }
}
