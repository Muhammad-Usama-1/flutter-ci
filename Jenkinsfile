pipeline {
    agent any

    stages {
        stage('GIT PULL') {
            steps {
                git branch: "develop",credentialsId: 'github_access', url: 'https://github.com/Muhammad-Usama-1/flutter-ci'
            }
        }
     
        stage('BUILD') {
            steps {
                 sh '''
                  #!/bin/sh
                  export ANDROID_HOME=var/lib/jenkins
                  export ANDROID_SDK_ROOT=/var/lib/jenkins
                  
                  flutter build apk --debug
                  '''
            
            }
        }
         stage('DISTRIBUTE') {
            steps {
                appCenter apiToken: 'app-center-api-key',
                        ownerName: 'appcenter-api',
                        appName: 'myapp',
                        pathToApp: 'build/app/outputs/apk/debug/app-debug.apk',
                        distributionGroups: 'myapp-group'
            }
        }
        
        
    }
}
