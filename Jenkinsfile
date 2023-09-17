pipeline {
  agent any
  stages {
    stage('Update dockerfile') {
      steps {
      script {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')])  {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email yeaktonghan.github@gmail.com"
                        sh "git config user.name yeaktonghan"
                        //sh "git switch master"
                        sh "sed -i 's+skymapled/simple-spring.*+skymapled/simple-spring:${DOCKERTAG}+g' app/spring-deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
          
        }
      }
      }
  }
}
}
}
