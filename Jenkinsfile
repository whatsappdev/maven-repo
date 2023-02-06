pipeline {

  agent { label 'slave1' }

  triggers {
  pollSCM '* * * * *'
}

  stages {
  
    stage ( 'scm checkout' ) { 
      steps {
        checkout scmGit(branches: [[name: '*/feat01']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/whatsappdev/maven-repo.git']])
}
}

    stage ( 'build') {
      steps {
        sh 'mvn package'
}
}

	stage ('uploadArtifactory') {
	  steps {
	    sh 'mvn deploy'
	  }
	}
	
	stage ('installApplication') {
	  steps {
	    sh 'scp /root/workspace/sample_pipeline/target/studentapp-2.1.1-FEAT01-SNAPSHOT.war root@172.31.10.29:/var/lib/tomcat/webapps'
	  }
	}
	
	stage ('postBuildNotification') {
	  steps {
	    emailext body: '$DEFAULT_CONTENT', subject: '$DEFAULT_SUBJECT', to: 'mlk.lucky836@gmail.com, siva.spring2021@gmail.com'
	  }
	}
	
} 
}
