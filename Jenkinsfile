// Define variable
def version = 'v0.9'

pipeline {
    agent any
    stages {
        stage('Git clone') {
           steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                userRemoteConfigs: [[url: 'git@github.com:welcomenews/do14.git']]])
           }    
        }    
    //    stage('Install nginx') {
    //        steps {
    //            sh 'sudo apt install nginx -y'    
    //        }
    //    }
   
        stage('Install Node') {   
            steps {
                sh 'curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash'
                sh 'source ~/.bashrc'
                sh 'nvm install v14.15.4'
            }    
        }
        stage('npm install') {   
            steps {
                sh 'cd nodejs.org && npm install'
            }    
        }
 /*       
        stage('Rewrate index-simlink') {
            when { expression { return fileExists ('/var/www/html/index-simlink') } }
            steps {
                sh "sudo ln -sfT /var/www/html/releases/$version/ /var/www/html/index-simlink"
                sh 'sudo systemctl reload nginx.service'
            }  
        }
        stage('Remove old versions\'s folders') {
            steps {
                sh 'cd /var/www/html/releases/'
                sh 'ls -dtr /var/www/html/releases/*/ | head -n -5 | sudo xargs -r rm -rf --'
            }
        }
*/
    }
}
