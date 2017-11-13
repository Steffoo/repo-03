<h1>Assignment 5</h1>
<h3>Einleitung</h3>
Ziel des Assignments ist es, den auf Maven umgestellten Tomcat-Build mit Hilfe
des CI-Tools "Jenkins" zu automatisieren. Wie diese Aufgabe bearbeitet wurde, wird
im folgenden beschrieben.
<h3>Ablauf</h3>
Zuallerst haben wir Jenkins auf dem Linux-Server installiert. Danach wurde eine
Jenkins-Pipeline angelegt, damit der Tomcat in Jenkins gebaut und
ausgeführt werden kann. Zum Schluss setzten wir einen Trigger, um zu
gewährleisten, dass bei jedem GitHub-Push der Tomcat gebuilded wird, ebenso
dass die Test ausgeführt werden und eine JAR-Datei abgelegt wird. Diese
Schritte werden im folgenden detailierter erläutert.
<h6>Jenkins-Installation<h6>
Im folgenden werden die Arbeitsschritte zur Installation des CI-Tools "Jenkins"
auf dem Linux-Server beschrieben. Vorraussetzung ist, dass man sich bereits
als root auf dem Linux-Server angemeldet hat.
1. Den Repository-Schlüssel dem System hinzugefügen: <br>
`
 sudo wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
`
2. Die Adresse des "Debian package repositories" in der "source.list"-Datei
des Linux-Servers hinzufügen: <br>
`
sudo echo deb https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list
`
3. Update ausführen, damit <i>apt-get</i> das neue Repository benutzt:
`
sudo apt-get update
`
4. Jenkisn und seine Abhängigkeiten installieren:
`
sudo apt-get install jenkins
`
5. Jenkins starten:
`
sudo systemctl start jenkins
`
Absofort läuft Jenkins unter <i>http://<Server-IP>:8080</i>
6. Weil Maven als Abhängigkeit gefehlt hat, haben wir es manuell installiert.
Wir haben uns dazu entschieden, Maven auf dem Linux-Server zu installieren und
nicht seperat in Jenkins:
`
sudo apt-get install maven
`

<h6>Jenkins-Konfiguration</h6>

<h6>Repository einbinden</h6>

<h6> Trigger setzten<h6>
  Webbhooks (fehlschlag)
  Tigger Pipeline hinzufügen

  <h6>Tests splitten</h6>
