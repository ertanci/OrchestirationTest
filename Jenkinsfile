pipeline {
  agent any
  stages {
    stage('one') {
      steps {
        echo "${myVar}" // prints 'initial_value'
        sh 'echo hotness > myfile.txt'
        script {
          echo "test"
          echo $(pwd)
          // OPTION 1: set variable by reading from file.
          // FYI, trim removes leading and trailing whitespace from the string
          myVar = readFile('myfile.txt').trim()
        }

        echo "${myVar}" // prints 'hotness'
      }
    }

    stage('two') {
      steps {
        echo "${myVar}" // prints 'hotness'
      }
    }

    stage('three') {
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
}