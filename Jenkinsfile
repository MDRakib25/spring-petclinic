pipeline {
    agent any

    // Trigger every 3 minutes on Thursdays (cron syntax: MINUTE HOUR DAY_OF_MONTH MONTH DAY_OF_WEEK)
    triggers {
        cron('H/3 * * * 4')  // '4' = Thursday (0-6, where 0=Sunday)
    }

    // Tools required for the pipeline (configure in Jenkins Global Tool Configuration)
    tools {
        maven 'M3'  // Name of Maven installation in Jenkins
        jdk 'JDK8'  // Name of JDK installation in Jenkins
    }

    stages {
        // Stage 1: Checkout code from GitHub
        stage('Checkout') {
            steps {
                checkout scm  // Checks out the code from your repository
            }
        }

        // Stage 2: Build and run tests with Maven
        stage('Build and Test') {
            steps {
                sh 'mvn clean package'  // Compiles, tests, and packages the app
            }
        }

        // Stage 3: Generate JaCoCo code coverage report
        stage('Code Coverage with JaCoCo') {
            steps {
                jacoco(
                    execPattern: 'target/jacoco.exec',        // Path to JaCoCo execution data
                    classPattern: 'target/classes',           // Compiled classes location
                    sourcePattern: 'src/main/java',           // Source code location
                    exclusionPattern: 'src/test/**'           // Exclude test files from coverage
                )
            }
        }
    }
}
