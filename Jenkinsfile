pipeline { 
   agent any
   options { 
	buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))
	}
   stages {
	stage('Unit Test') {
	  steps { 
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'

}

}     
	stage('Deploy') { 
	   steps { 
		sh 'cp dist/rectangle_${env.MAJOR_VERSION}.${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all'

}

}

stage('build') {
	steps {
		sh 'ant -f build.xml -v'
}
}
}
  post {
	always {
	  archiveArtifacts artifacts: 'dist/*.jar', fingerprint:true
}

}
}
