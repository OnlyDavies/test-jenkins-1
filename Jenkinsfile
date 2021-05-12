// comment
pipeline {
 agent any
 stages {
        stage('Checkout-git'){
               steps{
		git poll: true, url: 'git@github.com:OnlyDavies/test-jenkins-1.git'
               }
        }
        stage('CreateVirtualEnv') {
            steps {
				sh '''
					bash -c "virtualenv entorno_virtual && source entorno_virtual/bin/activate"
				'''

            }
        }
        stage('InstallRequirements') {
            steps {
            	sh '''
            		bash -c "source ${WORKSPACE}/entorno_virtual/bin/activate && ${WORKSPACE}/entorno_virtual/bin/pip install -r requirements.txt"
                '''
            }
        }   
        stage('TestApp') {
            steps {
            	sh '''
            		bash -c "source ${WORKSPACE}/entorno_virtual/bin/activate && ${WORKSPACE}/entorno_virtual/bin/pytest"
                '''
            }
        }  
        stage('RunApp') {
            steps {
            	sh '''
            		bash -c "source entorno_virtual/bin/activate ; ${WORKSPACE}/entorno_virtual/bin/python ${WORKSPACE}/scripts/src/main.py &"
                '''
            }
        } 
        stage('BuildDocker') {
            steps {
            	sh '''
            		docker build -t apptest:latest .
                '''
            }
        } 
    stage('PushDockerImage') {
            steps {
            	sh '''
            		docker tag apptest:latest onlydavies/apptest:latest
					docker push onlydavies/apptest:latest
					docker rmi apptest:latest
                '''
            }
        } 
  }
}

