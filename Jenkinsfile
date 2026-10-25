pipeline {

    agent any

<<<<<<< HEAD
    tools {
        jdk 'JDK21'
        maven 'Maven3.9'
        nodejs 'NodeJS22'
    }

    options {
        skipDefaultCheckout(true)
        disableConcurrentBuilds(abortPrevious: true)
        timeout(time: 30, unit: 'MINUTES')
    }

    stages {

        stage('Checkout Repository') {
            steps {
                checkout scm
            }
        }

        stage('Verify Files') {
            steps {
                bat '''
                    echo ========================================
                    echo CHECKING PROJECT STRUCTURE
                    echo ========================================

                    echo.
                    echo ===== ROOT =====
                    dir

                    echo.
                    echo ===== BACKEND =====
                    dir task-track

                    echo.
                    echo ===== FRONTEND =====
                    dir task_track-ui

                    echo.
                    echo ===== FRONTEND PACKAGE.JSON =====
                    dir task_track-ui\\package.json

                    echo.
                    echo ========================================
                    echo FILE VERIFICATION COMPLETED
                    echo ========================================
                '''
            }
        }

        stage('Build Backend') {
            steps {
                dir('task-track') {
                    bat '''
                        echo ========================================
                        echo BUILDING SPRING BOOT BACKEND
                        echo ========================================

                        mvn clean package -DskipTests

                        if errorlevel 1 (
                            echo.
                            echo BACKEND BUILD FAILED
                            exit /b 1
                        )

                        echo.
                        echo BACKEND BUILD SUCCESSFUL
                    '''
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('task_track-ui') {
                    bat '''
                        echo ========================================
                        echo BUILDING ANGULAR FRONTEND
                        echo ========================================

                        npm install

                        if errorlevel 1 (
                            echo.
                            echo NPM INSTALL FAILED
                            exit /b 1
                        )

                        npm run build

                        if errorlevel 1 (
                            echo.
                            echo FRONTEND BUILD FAILED
                            exit /b 1
                        )

                        echo.
                        echo FRONTEND BUILD SUCCESSFUL
                    '''
                }
            }
        }

        stage('Check Docker') {
            steps {
                bat '''
                    echo ========================================
                    echo CHECKING DOCKER
                    echo ========================================

                    docker version

                    if errorlevel 1 (
                        echo.
                        echo ERROR: DOCKER ENGINE IS NOT RUNNING
                        echo Please start Docker Desktop.
                        exit /b 1
                    )

                    echo.
                    echo DOCKER IS RUNNING
                '''
            }
        }

        stage('Docker Compose Build') {
            steps {
                bat '''
                    echo ========================================
                    echo BUILDING DOCKER IMAGES
                    echo ========================================

                    docker compose build --no-cache

                    if errorlevel 1 (
                        echo.
                        echo DOCKER BUILD FAILED
                        exit /b 1
                    )

                    echo.
                    echo DOCKER BUILD SUCCESSFUL
                '''
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                    echo ========================================
                    echo DEPLOYING APPLICATION
                    echo ========================================

                    docker compose down

                    if errorlevel 1 (
                        echo.
                        echo DOCKER COMPOSE DOWN FAILED
                        exit /b 1
                    )

                    docker compose up -d

                    if errorlevel 1 (
                        echo.
                        echo DOCKER COMPOSE UP FAILED
                        exit /b 1
                    )

                    echo.
                    echo APPLICATION DEPLOYED SUCCESSFULLY
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                bat '''
                    echo ========================================
                    echo VERIFYING DEPLOYMENT
                    echo ========================================

                    docker compose ps

                    if errorlevel 1 (
                        echo.
                        echo DEPLOYMENT VERIFICATION FAILED
                        exit /b 1
                    )

                    echo.
                    echo DEPLOYMENT VERIFICATION COMPLETED
                '''
            }
        }
=======
tools {
    maven 'Maven3.9'
    jdk 'JDK21'
}

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/akhileshkumar4953/working-track.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t working_track .'
            }
        }

>>>>>>> 1cea0b14c7129bd434ff4fef3af83baf955130fb
    }

    post {

        success {
<<<<<<< HEAD
            echo '========================================'
            echo 'APPLICATION SUCCESSFULLY DEPLOYED'
            echo '========================================'
        }

        failure {
            echo '========================================'
            echo 'DEPLOYMENT FAILED'
            echo '========================================'
        }

        aborted {
            echo '========================================'
            echo 'BUILD ABORTED'
            echo '========================================'
        }
    }
=======
            echo 'Build Successful'
        }

        failure {
            echo 'Build Failed'
        }

    }

>>>>>>> 1cea0b14c7129bd434ff4fef3af83baf955130fb
}