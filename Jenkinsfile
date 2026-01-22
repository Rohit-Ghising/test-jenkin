node{
  def appDir = '/var/www/nextjs-app'
  stage("Clean Workspace")
  {
    echo "Cleaning jenkins work"
    deleteDir()
  }
  stage("Clone Repositiry"){
    echo 'CLoning Reposthry'
    git (
      branch : 'main',
      url: 'https://github.com/Rohit-Ghising/test-jenkin'
    )
    stage("Deplot to EC2"){
    echo "Deploying to ec2"
    sh """
    sudo mkdir -p ${appDir}
    sudo chown -R 
    jenkins:jenkins ${appDir}
    rsync -av --deleteDir --exclude='.git' --exclude='node_modules' ./ ${appDir}
      
      cd ${appDir}
      sudo npm install
      sudo npm run build
      sudo fuser -k 3000/tcp || true
      npm run start
    """
    }


  }
}