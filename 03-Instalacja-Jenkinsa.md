Metoda tradycyjna:
```
sudo wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
sudo echo deb https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list
sudo apt-get update
sudo apt-get install jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```
Logowanie:
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword```
http://jenkins:8080
```
Instalacja jako kontener
```
docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts
```