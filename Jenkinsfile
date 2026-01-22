node {
    def appDir = '/var/www/nextjs-app'

    stage("Clean Workspace") {
        echo "Cleaning Jenkins workspace"
        deleteDir()
    }

    stage("Clone Repository") {
        echo 'Cloning Repository'
        git (
            branch: 'main',
            url: 'https://github.com/Rohit-Ghising/test-jenkin'
        )
    }

    stage("Deploy to EC2") {
        echo "Deploying to EC2"
        sh """
            # Create app directory and set permissions
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            # Sync files excluding .git and node_modules
            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

            # Go to app directory
            cd ${appDir}

            # Install dependencies and build
            sudo npm install
            sudo npm run build

            # Kill any process running on port 3000
            sudo fuser -k 3000/tcp || true

            # Start Next.js app in background
            nohup npm run start &>/dev/null &
        """
    }
}
