pipeline {
  agent any
  stages {
    stage('one') {
      environment {
        myname = 'myvalue'
      }
      parallel {
        stage('one') {
          steps {
            echo "${myVar}" // prints 'initial_value'
            sh 'echo hotness > myfile.txt'
            script {
              echo "test"
              // OPTION 1: set variable by reading from file.
              // FYI, trim removes leading and trailing whitespace from the string
              myVar = readFile('myfile.txt').trim()
            }

            echo "${myVar}" // prints 'hotness'
          }
        }

        stage('parallel for one') {
          steps {
            echo 'I am for parallel one '
            retry(count: 3) {
              echo 'retry this'
            }

          }
        }

      }
    }

    stage('two') {
      steps {
        echo "${myVar}" // prints 'hotness'
      }
    }

    stage('https://emojipedia.org/ship/ three') {
      when {
        expression {
          myVar != 'hotness'
        }

      }
      steps {
        echo "three: ${myVar}"
      }
    }

  }
  environment {
    myVar = 'ertan'
  }
}