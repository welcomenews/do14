// Define variable
def version = 'v0.9'

pipeline {
    agent { label 'agent1' }
    stages {
        stage('Git clone') {
           steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']],
                //userRemoteConfigs: [[url: 'git@github.com:welcomenews/do14.git']]])
                userRemoteConfigs: [[url: 'https://github.com/nodejs/nodejs.org.git']]])
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
                sh 'mkdir ~/.bashrc ; . ~/.bashrc'
                sh 'bash -l -c ". $HOME/.nvm/nvm.sh ; nvm install v14.15.4 && nvm use v14.15.4"' 
                //sh '. ~/.bashrc'
                //sh '. ~/.nvm/nvm.sh'
            }    
        }
 
        stage('npm install') {   
            steps {
//                sh 'cd /var/lib/jenkins/workspace/do-14Pre && npm install ; npm run build'
                sh 'cd /var/lib/jenkins/workspace/workspace/do-14Pre && npm install ; npm run build'
//                sh 'ls -l /var/lib/jenkins/workspace/do-14Pre'
                archiveArtifacts artifacts: 'build/', fingerprint: true
            }    
        }
        
//    post {
//        always {
//            archiveArtifacts artifacts: 'build/', fingerprint: true
//        }    
//    }
//        stage('pull artifact') {
//            steps {
//                copyArtifacts filter: 'build/', fingerprintArtifacts: true, target: '/var/www/html/index-simlink/'
//            }
//        }        
        
        stage('Copy static site') {
            steps {
                sh "sudo mkdir -p /var/www/html/releases/$version"
//                sh "sudo cp -rf /var/lib/jenkins/workspace/do-14Pre/build/ /var/www/html/releases/$version"
                sh "sudo cp -rf /var/lib/jenkins/workspace/workspace/do-14Pre/build/ /var/www/html/releases/$version"
                sh "sudo chown -R www-data:www-data /var/www/html/releases/$version/*"
           }
        }
        
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
    } 
}
