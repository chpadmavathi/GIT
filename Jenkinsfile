pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
    agent none
      stages{
           stage('Checkout'){
               agent any
               steps{
		 echo 'cloning..'
                 git 'https://github.com/Sonal0409/DevOpsClassCodes.git'
              }
          }
        stage('Deploy'){
      agent any
      steps{
        sh label: '', script: '''rm -rf mydockerfile
mkdir mydockerfile
cd mydockerfile
touch dockerfile
cat <<EOT>> dockerfile
FROM ubuntu
RUN apt-get update
RUN apt-get install nginx -y
COPY index.html /var/www/html/
EXPOSE 80
CMD ["nginx","-g","daemon off;"]
EOT
sudo docker build -t myimage:$BUILD_NUMBER .
sudo docker run -itd -P myimage:$BUILD_NUMBER'''
      }
    }
        
      }
  
}
