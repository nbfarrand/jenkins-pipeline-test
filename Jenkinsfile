podTemplate(containers: [
    containerTemplate(name: 'golang', image: 'golang:1.16.3', ttyEnabled: true, command: 'cat')
  ]) {

    node(POD_LABEL) {
        container('golang') {
            stage('Pre Test') {
                echo 'Installing dependencies'
                sh 'go version'
                sh 'go get -u golang.org/x/lint/golint'
            }

            stage('Build') {
                echo 'Compiling and building'
                sh 'echo Workspace dir is ${pwd()}'
                sh 'ls -al'
                sh 'go build'
            }

            stage('Test') {
                echo 'Running vetting'
                sh 'go vet .'
                echo 'Running linting'
                sh 'golint .'
                echo 'Running test'
                sh 'go test -v'
            }
        }
    }
 }