Pipeline {
   agent any

stgaes {
  stage("cloning the code") {
    steps {
        git branch: 'main', url: 'https://github.com/chandu1861/practice.git'
    }
  }

  stage ("build the docker image") {
    steps {
        sh docker build -t image .
    }
  }

  stage ("creating container") {
    steps {
       sh docker run -it --name c1 -p 9000:80 image /bin/bash
    }
  }

  stage ("login to docker") {
    steps {
        withCredentials([usernamePassword(credentialsId: '', passwordVariable: 'docker_password', usernameVariable: 'docker_username')]) {
        sh docker push chandana1213/img:latest

        }
    }
  }
}
  }
