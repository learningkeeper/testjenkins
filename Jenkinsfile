def now = new Date()
def myUrl='github.com/learningkeeper/testjenkins.git'

node {


    stage('pull code') {
        //sh "git config --global credential.helper cache"
        //sh 'git config --global push.default simple'
        checkout([$class: 'GitSCM', 
        branches: [[name: '*/main']], 
        extensions: [],
        userRemoteConfigs: [[credentialsId: 'joe-git', url: 'https://' + (myUrl) ]]])
        try {
        sh "git fetch && git checkout main && git pull"
        sh "echo \$(date +%s) >> 1.txt"
        sh "git add ."
        sh '''git commit -m "add ${GIT_COMMIT}"'''
       
        withCredentials([usernamePassword(credentialsId: 'joe-git',
        usernameVariable: 'username',
        passwordVariable: 'password')]){
        sh("git push http://$username:$password@$myUrl")
        }
        } catch(e) {
            print(e)
        }
            
    }
        
        
    
}

