podTemplate(containers: [
//     containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'golang', image: 'golang:1.16.3', ttyEnabled: true, command: 'cat')
  ]) {

    node(POD_LABEL) {
//         stage('Get a Maven project') {
//             git 'https://github.com/jenkinsci/kubernetes-plugin.git'
//             container('maven') {
//                 stage('Build a Maven project') {
//                     sh 'mvn -B clean install'
//                 }
//             }
//         }

//         stage('Get a Golang project') {
//             git url: 'https://github.com/hashicorp/terraform.git'
//             container('golang') {
//                 stage('Build a Go project') {
//                     sh """
//                     mkdir -p /go/src/github.com/hashicorp
//                     ln -s `pwd` /go/src/github.com/hashicorp/terraform
//                     cd /go/src/github.com/hashicorp/terraform && make core-dev
//                     """
//                 }
//             }
//         }

        stage('Pre Test') {
            steps {
                echo 'Installing dependencies'
                sh 'go version'
                sh 'go get -u golang.org/x/lint/golint'
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling and building'
                sh 'go build'
            }
        }

        stage('Test') {
            steps {
                withEnv(["PATH+GO=${GOPATH}/bin"]){
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