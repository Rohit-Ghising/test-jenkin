// Ktt2BF0zay778cl6xdOTXJXB

pipelinee{
  agent any
  environment {
    VERCEL_TOKEN = credentials ('vercel_token')
  }
  stages{
    stage('Install'){
      steps{
        bat 'npm install'
      }
    }
    stage('Test'){
      steps{
        echo "Skipping test"
      }
    }
    stage('build'){
      steps{
        bat 'npm run build'
      }
    }
     stage('Deploy'){
      steps{
        bat 'npx vecel --prod --yes --token=% VERCEL_TOKEN%'
      }
    }
    }
  }


