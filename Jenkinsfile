pipeline {
    
    agent any
    
    environment {
        REACT_DEPLOYMENT_STATUS = sh(script: "helm get react-frontend", returnStatus: true)
    }
    
    stages {
        
        stage("Deploy React Frontend") {
            when {
                expression {env.REACT_DEPLOYMENT_STATUS == "1"}
            }
            steps {
                echo "Deploy React"
                sh 'helm install --name react-frontend --namespace react-frontend .'
            }
        }
        
        stage("Upgrade React Frontend") {
            when {
                expression {env.REACT_DEPLOYMENT_STATUS == "0"}
            }
            steps {
                echo "Upgrade React"
                sh 'helm upgrade react-frontend .'
            }
        }
    }
}
