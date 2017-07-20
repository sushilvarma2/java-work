pipeline { 
   agent any
   options { 
	buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))
	}
   stages {
	stage('Unit Test') {
	  agent { 
		label 'apache'
		}
	  steps { 
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'

}

}     
stage('build') {
        agent {
                label 'apache'
                }


        steps {
                sh 'ant -f build.xml -v'
}
}
	stage('Deploy') { 
		agent {
                	label 'apache'
                }

	   steps { 
		sh 'cp dist/rectangle.jar /var/www/html/rectangles/all'

}

}

	stage('Running on apache') { 
	agent { label 'apache'  }		
 	steps { 
	sh "wget http://varmasushil5.mylabserver.com/rectangles/all/rectangle.jar"
	sh "java -jar rectangle.jar 4 5"
}

}
stage('Promote to Green') {
        agent { 
		label 'apache'  
	      }
        steps {
        sh "cp /var/www/html/rectangles/all/rectangle.jar /var/www/html/rectangles/green/rectangle.jar"
}

}


}
  post {
	always {
	  archiveArtifacts artifacts: 'dist/*.jar', fingerprint:true
}

}
}
