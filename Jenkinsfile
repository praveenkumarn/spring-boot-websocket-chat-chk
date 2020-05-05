// Powered by Infostretch 

timestamps {

node ('Docker') { 

	deleteDir()
	stage ('Docker_Push - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'GitHub', url: 'https://github.com/praveenkumarn/spring-boot-websocket-chat-demo']]]) 
	}
	stage ('Docker_Push - Build') {
 	
// Unable to convert a build step referring to "hudson.plugins.ws__cleanup.PreBuildCleanup". Please verify and convert manually if required.		// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn -f pom.xml clean package " 
			} else { 
 				bat "mvn -f pom.xml clean package " 
			} 
 		}		// Shell build step
sh ''' 
#!/bin/bash
pwd
id
ls -lrt
java -version


sudo -S docker image ls
sudo -S docker container ls

sudo -S docker stop $(sudo -S docker ps -a -q)
sudo -S docker rm $(sudo -S docker ps -a -q)

sudo  -S  docker images | egrep "latest|SNAPSHOT" | awk '{print $1 ":" $2}' | xargs sudo -S  docker rmi -f

sudo -S docker build -t spring-boot-websocket-chat-demo .
sudo -S docker run -d -p 4000:8080 spring-boot-websocket-chat-demo

sudo -S docker image ls
sudo -S docker container ls


sudo -S docker tag spring-boot-websocket-chat-demo praveenkumarnagarajan/spring-boot-websocket-chat-demo:0.0.1-SNAPSHOT

cat ~/pass.txt | sudo -S docker login --username praveenkumarnagarajan --password-stdin

sudo -S docker push praveenkumarnagarajan/spring-boot-websocket-chat-demo:0.0.1-SNAPSHOT 


docker pull praveenkumarnagarajan/spring-boot-websocket-chat-demo:0.0.1-SNAPSHOT


docker image ls

kubectl run kubernetes-springboot --image=praveenkumarnagarajan/spring-boot-websocket-chat-demo:0.0.1-SNAPSHOT --port=8080

kubectl expose deployment/kubernetes-springboot --type="NodePort" --port 8080


kubectl get nodes

kubectl get services

kubectl describe services/kubernetes-springboot


""" 


 ''' 
	}
}
}
