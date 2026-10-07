pipeline {
    agent {
        label 'linux'
    }

    stages {

        stage('Detect Branch') {
            steps {
                echo "Current Branch = ${env.BRANCH_NAME}"
                echo "Job Name       = ${env.JOB_NAME}"
                echo "Build Number   = ${env.BUILD_NUMBER}"
            }
        }

        stage('Branch Decision') {
            steps {
                script {

                    if (env.BRANCH_NAME == 'main') {

                        echo 'Main branch detected'
                        echo 'Production deployment allowed'

                    } else if (env.BRANCH_NAME == 'develop') {

                        echo 'Develop branch detected'
                        echo 'Deploy to staging'

                    } else if (env.BRANCH_NAME.startsWith('feature-')) {

                        echo 'Feature branch detected'
                        echo 'Build and Test only'

                    } else {

                        echo "Other branch detected: ${env.BRANCH_NAME}"
                    }
                }
            }
        }

        stage('Production Deploy') {
            when {
                branch 'main'
            }

            steps {
                echo 'PRODUCTION DEPLOYMENT STAGE EXECUTED'
            }
        }

        stage('Staging Deploy') {
            when {
                branch 'develop'
            }

            steps {
                echo 'STAGING DEPLOYMENT STAGE EXECUTED'
            }
        }
    }
}
