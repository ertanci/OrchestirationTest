myVar = 'initial_value'

pipeline {
  agent any
  stages {
    stage('one') {
      steps {
        echo "${myVar}" // prints 'initial_value'
        sh 'echo hotness > myfile.txt'
        script {
            echo "test"
          // OPTION 1: set variable by reading from file.
          // FYI, trim removes leading and trailing whitespace from the string
          myVar = readFile('myfile.txt').trim()

          // OPTION 2: set variable by grabbing output from script
          //sh 'ssh ertan@c1.ansible.com'
          //myVar = sh(script: '/home/ertan/bScript.sh', returnStdout: true).trim()
        }
        echo "${myVar}" // prints 'hotness'
      }
    }

    stage('two') {
      steps {
        echo "${myVar}" // prints 'hotness'
      }
    }
    // this stage is skipped due to the when expression, so nothing is printed
    stage('three') {
      when {
        expression { myVar != 'hotness' }
      }
      steps {
        echo "three: ${myVar}"
      }
    }
  }
}
