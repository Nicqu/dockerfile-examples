#!/usr/bin/env groovy

node ('dockerserver') {
        stage "build"
        checkout scm
        def customImage = docker.build("docker-image:${env.BUILD_ID}", "-f ./apache/Dockerfile .")
        
        stage "test copying files"
        customImage.inside('-v $WORKSPACE:/output -u root') {
            /* Run some tests which require MySQL */
            sh """
            ls /output
            touch /app/test.html && ls /app
            cp /app/test.html /output
            """ 
        }
        archiveArtifacts artifacts: '*.html'
}
