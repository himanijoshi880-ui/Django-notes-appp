pipeline{
    agent any
    stages{
        stage ("code"){
            steps{
                echo "clonning the code"
                git url: "https://github.com/himanijoshi880-ui/Django-notes-appp.git" , branch : "main"
            }
        }
        stage ("build"){
              steps{
                  echo "building the code"
                  sh "docker build -t my-notes-app ."
            }
        }
        stage ("pushing"){
              steps{
                  echo "pussing image to docker hub" 
                  withCredentials([usernamePassword(credentialsId: "dockerHub" , usernameVariable : "dockerUsername" , passwordVariable: "dockerPass")]) {
                  sh "docker tag my-notes-app ${dockerUsername}/my-notes-app"
                  sh "docker login -u ${dockerUsername} -p ${dockerPass} "    
                  sh "docker push ${dockerUsername}/my-notes-app"
                     }
              }
        }
        stage ("deployment"){
              steps{
               echo "deployment" 
               sh " docker compose down && docker compose up -d "
            }
        }
    }
}
