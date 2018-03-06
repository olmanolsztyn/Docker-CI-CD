Tworzymy w repozytorium plik .Jenkinsfile:
```
#!/usr/bin/env groovy

pipeline {

    agent {
        node {
            lebel 'swarm-ci'
        }
    }
    
    environment {
        REGISTRY_ADDRESS = "master0"
        DEPLOY_URL = "http://master0:8080"
        COMPOSE_FILE = "docker-compose.yml"
        STACK_PREFIX = "cmentarnapolka-stack"
    }
    
    stages {
        stage('Build') {
            steps {
                sh "docker login ${env.REGISTRY_ADDRESS}"
                sh "docker-compose -f ${env.COMPOSE_FILE} build"
                sh "docker-compose -f ${env.COMPOSE_FILE} push"
            }
        }
        stage('Deploy') {
            steps {
                sh "docker login ${env.REGISTRY_ADDRESS}"
                sh "docker stack deploy ${env.DEPLOY_STACK_NAME} -c ${env.COMPOSE_FILE}"
            }
        }
    }
}
```