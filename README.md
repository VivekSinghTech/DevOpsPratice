# Vivek CI/CD Demo

GitHub -> Jenkins -> Docker -> Nginx -> AWS EC2

## Local run

docker build -t vivek-web .
docker run -d --name vivek-web -p 8081:80 vivek-web

Open http://localhost:8081

## Jenkins

Create a Pipeline job pointing to this repository. Keep Jenkinsfile in the repository root.

The pipeline checks out code, builds the Docker image, deploys the container on port 8081, and verifies it with curl.

Jenkins needs Docker access:
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
