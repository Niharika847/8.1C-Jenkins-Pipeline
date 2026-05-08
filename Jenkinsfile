pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *') // Poll GitHub every 5 minutes for new commits
    }

    stages {

        stage('Build') {
            steps {
                echo '========== Stage 1: Build =========='
                echo 'Task: Compiling and packaging the application source code.'
                echo 'Tool: Maven - a build automation tool used for Java projects.'
                echo 'Command: mvn clean package'
                echo 'This stage compiles all source files and produces a deployable artifact (e.g., .jar or .war).'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo '========== Stage 2: Unit and Integration Tests =========='
                echo 'Task: Running unit tests to validate individual components and integration tests to verify component interactions.'
                echo 'Tools:'
                echo '  - JUnit: Unit testing framework for Java applications.'
                echo '  - Selenium: Integration testing framework for UI/end-to-end testing.'
                echo 'Commands: mvn test (unit) | mvn verify (integration)'
                echo 'This stage ensures individual code units function correctly and components work together as expected.'
            }
        }

        stage('Code Analysis') {
            steps {
                echo '========== Stage 3: Code Analysis =========='
                echo 'Task: Analysing source code for quality issues, code smells, and adherence to industry coding standards.'
                echo 'Tool: Checkstyle - a static code analysis tool that checks Java code against a defined ruleset.'
                echo 'Command: mvn checkstyle:check'
                echo 'This stage enforces coding standards and identifies maintainability issues before deployment.'
            }
        }

        stage('Security Scan') {
            steps {
                echo '========== Stage 4: Security Scan =========='
                echo 'Task: Scanning the application and its dependencies for known security vulnerabilities (CVEs).'
                echo 'Tool: OWASP Dependency-Check - identifies publicly disclosed vulnerabilities in project dependencies.'
                echo 'Command: dependency-check.sh --project MyApp --scan . --format HTML'
                echo 'This stage identifies security risks in third-party libraries used by the application.'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo '========== Stage 5: Deploy to Staging =========='
                echo 'Task: Deploying the packaged application artifact to a staging server for pre-production testing.'
                echo 'Tool: AWS CLI - command-line interface for interacting with AWS services such as EC2.'
                echo 'Command: aws s3 cp target/app.jar s3://staging-bucket/ && ssh ec2-user@staging-ec2 "sudo systemctl restart app"'
                echo 'This stage deploys the application to an AWS EC2 staging instance that mirrors the production environment.'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo '========== Stage 6: Integration Tests on Staging =========='
                echo 'Task: Running integration tests on the live staging environment to ensure the application behaves correctly in production-like conditions.'
                echo 'Tool: Postman/Newman - API testing tool that runs automated API test collections.'
                echo 'Command: newman run staging-tests.json --environment staging-env.json'
                echo 'This stage validates end-to-end application functionality against the staging server before production deployment.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo '========== Stage 7: Deploy to Production =========='
                echo 'Task: Deploying the fully tested and verified application to the live production server.'
                echo 'Tool: AWS CLI - used to deploy to the production AWS EC2 instance.'
                echo 'Command: aws s3 cp target/app.jar s3://production-bucket/ && ssh ec2-user@prod-ec2 "sudo systemctl restart app"'
                echo 'This stage performs the final deployment to the production environment, making the application available to end users.'
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed successfully! All 7 stages passed.'
        }
        failure {
            echo 'Pipeline failed. Please review the stage output above.'
        }
    }
}
