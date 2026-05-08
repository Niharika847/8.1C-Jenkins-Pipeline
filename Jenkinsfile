pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *') // Poll GitHub every 5 minutes for new commits
    }

    stages {

        stage('Checkout') {
            steps {
                echo '========== Checking out source code from GitHub =========='
                git branch: 'main', url: 'https://github.com/YOUR_GITHUB_USERNAME/8.2CDevSecOps.git'
                echo 'Source code checked out successfully.'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo '========== Installing Node.js dependencies =========='
                sh 'npm install'
                echo 'All dependencies installed via npm.'
            }
        }

        stage('Run Tests') {
            steps {
                echo '========== Running application test suite =========='
                sh 'npm test || true' // Allows pipeline to continue despite test failures
                echo 'Test stage complete.'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                echo '========== Generating code coverage report =========='
                sh 'npm run coverage || true'
                echo 'Coverage report generated (if script exists).'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                echo '========== Running NPM Security Audit =========='
                sh 'npm audit || true' // Shows known CVEs in the output
                echo 'Security audit complete. Review above output for vulnerabilities.'
            }
        }

    }

    post {
        success {
            echo 'DevSecOps pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline encountered an error. Check stage output above.'
        }
    }
}
