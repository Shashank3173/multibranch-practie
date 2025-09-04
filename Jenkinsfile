// pipeline {
//     agent any

//     stages {
//         stage('Checkout') {
//             steps {
//                 checkout scm
//             }
//         }

//         stage('Build') {
//             steps {
//                 echo "Building project on branch: ${env.BRANCH_NAME}"
//             }
//         }

//         stage('Test') {
//             steps {
//                 echo "Running tests for branch: ${env.BRANCH_NAME}"
//             }
//         }

//         stage('Deploy') {
//             steps {
//                 echo "Deploying branch: ${env.BRANCH_NAME}"
//                 // Example: deploy different branches to different locations
//                 script {
//                     if (env.BRANCH_NAME == 'master') {
//                         echo "Deploying to Production Server"
//                     } else {
//                         echo "Deploying to Staging/Dev Server"
//                     }
//                 }
//             }
//         }
//     }
// }
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    if (env.CHANGE_ID) {
                        echo "This is a PR build. PR Number: ${env.CHANGE_ID}"
                    } else {
                        echo "This is a normal branch build. Branch: ${env.BRANCH_NAME}"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    if (env.CHANGE_ID) {
                        echo "Skipping deploy for PR..."
                    } else if (env.BRANCH_NAME == 'master') {
                        echo "Deploying to Production..."
                    } else {
                        echo "Deploying to Staging..."
                    }
                }
            }
        }
    }
}
