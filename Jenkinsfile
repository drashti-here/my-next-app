pipeline {
  agent any

  environment {
    NODE_ENV = 'production'
  }

  tools {
    nodejs 'Node 22' // make sure Jenkins has this tool named "Node 18"
  }

  stages {
    stage('Clone Repo') {
      steps {
        git url: 'https://github.com/your-username/your-repo.git', branch: 'main'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Build Next.js App') {
      steps {
        sh 'npm run build'
      }
    }

    stage('Export Static Site') {
      steps {
        sh 'npm run export'
      }
    }

    stage('Deploy (optional)') {
      when {
        branch 'main'
      }
      steps {
        // Replace this with your own SCP/Rsync step
        sh '''
          echo "Deploying to remote server..."
          scp -r out/* user@yourserver.com:/var/www/your-site/
        '''
      }
    }
  }

  post {
    success {
      echo "✅ Build and deploy successful!"
    }
    failure {
      echo "❌ Build failed."
    }
  }
}
