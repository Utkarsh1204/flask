pipeline {
    agent any
    stages {
        stage ('SCM checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Utkarsh1204/flask.git'
            }
        }
        stage ('docker image build') {
            steps {
                sh '/usr/bin/docker image build -t switchblade1204/flaskimage .'
            }
        }
        stage ('docker login') {
            steps {
                sh 'echo  dckr_pat_H9d8UbnyH-1BhTgI2OhAiVtn5N0 | /usr/bin/docker login -u switchblade1204 --password-stdin'
            }
        }
        stage ('docker image push') {
            steps {
                sh '/usr/bin/docker image push switchblade1204/flaskimage'
            }
        }
        stage ('get the confirmation from user') {
            steps {
                input 'Do you want to deploy this application?'
            }
        }
        stage ('remove existing service') {
            steps {
                sh '/usr/bin/docker service rm flask-service'
            }
        }
        stage ('create docker service') {
            steps {
                sh '/usr/bin/docker service create --name flask-service -p 4000:4000 --replicas 2 switchblade1204/flaskimage'
            }
        }
        
    }
}
