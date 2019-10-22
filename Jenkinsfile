pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Git') { 
            steps { 
                sh 'rm -rf my_php'
                sh 'git clone https://github.com/sbaron81/my_php.git'
            }
        }
        stage('Copy'){
            steps {
                sh 'rm -rf ~/www/*'
                sh 'cp my_php/index.php ~/www'
                sh 'chmod 777 ~/www/*'
            }
        }
        stage('Remove old version') {
            steps {
                sh 'docker container rm -f my_php'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d --name my_php -p 8888:80 -v ~/www:/var/www/html php:7.2-apache'
            }
        }
    }
}
