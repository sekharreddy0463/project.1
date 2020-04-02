pipeline {
    agent any

    stages {
        stage("Fetch repository") {
            steps {
                    git 'https://github.com/chandra635313/javawar.git'
                }
            }
            stage('Build') { 
            steps {
                 sh 'mvn -f pom.xml clean install'
            }
        }
        
        stage('Test') { 
            steps {
                  sh 'mvn -f pom.xml test'
                  
            }
        }
        
        stage('upload artifacts'){
            steps{
                s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'myaws1656', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'ap-south-1', showDirectlyInBrowser: false, sourceFile: '**/webapp/target/*war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false, userMetadata: [[key: '', value: '']]]], pluginFailureResultConstraint: 'FAILURE', profileName: 'devops-jenkins', userMetadata: []
            }
        }
        stage('deploy code'){
        steps{
        deploy adapters: [tomcat8(credentialsId: 'tomcat.crediantls', path: '', url: 'http://13.233.38.179:8080/')], contextPath: null, war: '**/*.war'
        }
    }
    }
}
            
