// Define variable
def version = 'v0.9'

pipeline {
    agent any
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
   
     ///   stage('Install Node') {   
        ///    steps {
      ///          sh 'curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash'
           //     sh 'sudo chmod u+x /var/lib/jenkins/.nvm/nvm.sh'
           //     sh "export NVM_DIR=$HOME/.nvm"
           //     sh ". $NVM_DIR/nvm.sh"
    ///            sh 'bash -l -c ". $HOME/.nvm/nvm.sh ; nvm install v14.15.4 && nvm use v14.15.4"' 
                //sh '. ~/.bashrc'
                
                //sh '. ~/.nvm/nvm.sh'
              //sh 'nvm install v14.15.4'
      ///      }    
  ///      }
        stage('npm install') {   
            steps {
                sh 'cd /var/lib/jenkins/workspace/do-14Pre && npm install ; ls -l /var/lib/jenkins/workspace/do-14Pre ; npm run build'
                sh 'ls -l /var/lib/jenkins/workspace/do-14Pre'
                archiveArtifacts artifacts: 'build/', fingerprint: true
            }    
        }
        
//        stage('Get artifact') {   
//            steps {
        
//    post {
//        always {
//            archiveArtifacts artifacts: 'build/', fingerprint: true
//        }    
//    }
        stage('pull artifact') {
            steps {
                copyArtifacts filter: 'build/', target: '/var/www/html/index-simlink/']);
            }
        }        
        
     //   stage('Rewrate index-simlink') {
      //      when { expression { return fileExists ('/var/www/html/index-simlink') } }
      //      steps {
       //         sh "sudo ln -sfT /var/www/html/releases/$version/ /var/www/html/index-simlink"
     //           sh 'sudo systemctl reload nginx.service'
     //       }  
     //   }
     //   stage('Remove old versions\'s folders') {
     //      steps {
     //           sh 'cd /var/www/html/releases/'
      //          sh 'ls -dtr /var/www/html/releases/*/ | head -n -5 | sudo xargs -r rm -rf --'
     //       }
     //   }
  
    
}
