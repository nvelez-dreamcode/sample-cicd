pipeline {
    
    agent {
        node {
            label 'nodejs-slave'
        }
    }

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
            )
    }

    stages {

        /*stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }*/

        stage('Tools Setup') {
            steps {                
                echo 'Validando git...'
                sh "git --version"
                echo 'Validando NodeJs...'
                sh "node -v"
                echo 'Validando npm...'
                sh "npm -v"
                echo 'Validando Java...'
                sh "java -version"
                echo 'Validando Terraform...'
                sh "terraform --version"
                echo 'Validando Gradle...'
                sh "gradle -v -g gradle-user-home"
            }
        }
        
        stage(' Unit Testing') {
            steps {                
                echo "Running Unit Tests"
                //sh "cd sample-app;npm test"
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                echo "Running Code Analysis"
                """
            }
        }
        
        stage('Deploy to Dev') {
            when {
                branch 'develop'
            }
            steps {
                echo "Deploying to Dev. environment from $BRANCH_NAME branch to $CHANGE_TARGET branch..."
            }
        }

        stage('Deploy to Test') {
            when {
                branch 'stage'
            }
            steps {
                echo "Deploying to Test environment from $BRANCH_NAME branch..."
            }
        }
        
        stage('Deploy to Production') {
            when {
                branch 'master'
            }
            steps {
                echo "Deploying to Production environment from $BRANCH_NAME branch..."
            }
        }
        
        /*stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                echo "Packaging and deploying Serverless artifacts..."
                //echo "BranchName: $BRANCH_NAME"
                samDeploy([
                    credentialsId: 'aws-fchaves-devops',
                    kmsKeyId: '',
                    outputTemplateFile: '',
                    region: 'us-east-1',
                    roleArn: '',
                    s3Bucket: 'sample-cicd-s3bucket2-devops',
                    s3Prefix: '',
                    stackName: 'dev',
                    templateFile: 'template.yaml'])
            }
        }*/


    }

}
