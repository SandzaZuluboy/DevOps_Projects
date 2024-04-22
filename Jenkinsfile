pipeline {
    agent {label 'maven'}

environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
}
    stages {
       stage("build"){
       steps {
           echo "-------------- build started ------------"
           sh  'mvn clean deploy -Dmaven.test.skip=true'
           echo "-----------build completed ----------"
       }

    }
    stage("test"){
        steps{
            echo "-----------unit test started ---------"
            sh 'mvn surefire-report:report'
            echo "---------unit test completed ----------"
        }
    }

    stage('sonarQube analysis') {
    environment{
        scannerHome = tool 'sandile-zulu-sonar-scanner' //sonar scanner name should be the same as what we have defined in the tools.
    }

    steps {                                           // in the steps we are adding our sonar qube server that is with Sonar Qube environment.
    withSonarQubeEnv('sandile-zulu-sonarqube-server') {

        sh "${scannerHome}/bin/sonar-scanner" // This is going to communicate with our sonar qube server and send the analysis report

    }
    }
  }
}
}