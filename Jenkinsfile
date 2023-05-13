pipeline{
 agent {label "dev-server" } 
 stages{
	stage("Clone Code"){
		steps{
		 git url: "https://github.com/bc2003065/node-todo-cicd.git", branch: "master"
		}
	}
	stage("Build and Test"){
	    steps{
		   echo "Docker will build and test this"
		   sh "docker build . -t node-app-test-pipeline"
		}
	}
	stage("Push to Docker Hub"){
		steps{
		    withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
		   echo "Docker hub recieve will the image"
		   sh "docker tag node-app-test-pipeline ${env.dockerHubUser}/node-app-test-pipeline:latest"
		   sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
		   sh "docker push ${env.dockerHubUser}/node-app-test-pipeline:latest"
		    }
		}
	}
	stage("Deploy"){
		steps{
		    echo "Docker compose will deploy this"
		    sh "docker-compose down && docker-compose up -d"
		}
	}
}
}
