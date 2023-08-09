pipeline{
    agent{ label 'dev-agent' }
    
        stages{
            stage('code'){
                steps {
                    git url: 'https://github.com/satyadeepS7/node-todo-cicd.git', branch: 'master' 
                }
            }
            stage('build and test'){
                steps {
                    sh "docker build . -t satyadeeps7/node-todo-app-cicd:latest"
                }
            }   
            stage('login and push image'){
                steps {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerHubPassword')]) {
                        sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                        sh "docker image push satyadeeps7/node-todo-app-cicd:latest"
                
                    }
                }
            }   
            stage('deploy'){
                steps {
                    sh "docker-compose down && docker-compose up -d"
                }
            }
        }
    }
