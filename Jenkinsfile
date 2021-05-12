pipeline {

  agent any

  stages {

    stage('Checkout-git'){

      steps{
        git poll: true, url: 'git@github.com:OnlyDavies/test-jenkins-1.git'
      }
    }

    stage('CreateVirtualEnv'){

      steps{
 
        sh '''

          bash -c "virtualenv entorno_virtual && source entorno_virtual/bin/activate"

        '''

      }

    }

    stage('InstallRequirements'){

      steps{

        sh '''

          bash -c "source entorno_virtual/bin/activate && entorno_virtual/bin/python /entorno_virtual/bin/pip install -r requirements.txt 
       
         '''
      }
 
    }

    stage('TestApp'){

      steps{

        sh '''

          bash -c "source entorno_virtual/bin/activate; entorno_virtual/bin/python scripts/src/main.py &"
     
        '''

      }

    }

  }

}
