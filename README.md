# android-jenkins-docker
Docker image with Jenkins that can build Android apps.

# Building the image
Run the command
>docker build -t android-jenkins .

# Run the image
Run the command
>docker run --name android-jenkins -p 8080:8080 -p 50000:50000 -v SOME_HOST_PATH:/var/jenkins_home android-jenkins

Replace ```SOME_HOST_PATH``` with the path to a folder on your host system where you want Jenkins to store its builds and configurations, for example ```/var/android_jenkins_home``` on Linux systems. If port 8080 is already used by another process on your host, you can modify which port redirects to Jenkins. If you want Jenkins to be accessible on port 8090 on your host, then replace the port argument with ```8090:8080``` in the run command.

## Windows tips
Setting the host path for ```jenkins_home``` is a bit tricky on Windows hosts. First of all, you probably need to share the drive where the folder lives and [this resource explains how](https://rominirani.com/docker-on-windows-mounting-host-directories-d96f3f056a2c#.7ec1d330n). Then, you need to provide the path with forward slashes, for example ```c:/Users/myuser/android_jenkins_home:/var/jenkins_home```

# Accessing Jenkins
Point your browser to http://localhost:8080 (or whichever port you bound) and configure your build.

## Gradle tips
If you are using gradle to build your project, you will want to configure the build to use the gradle wrapper. If you just want to create apks, then set the task to ```assembleDebug``` or ```assembleRelease```. Finally, add ```-x lint``` to the switches section to avoid lint from creating errors and disrupting the build.

# Modifying the image
Just modify the Dockerfile in case you want to modify the environment, for example
* Android SDK version
* Buildtools version
* Jenkins plugins

PRs are welcome for example for simplifying the mechanism for installing multiple buildtools versions.

docker run --name jenkins_24_android -u root -p 8001:8080 -p 50000:50000 -v /tools/android/jk-docker-file/jk_home:/var/jenkins_home jenkins_24_android



*************************************************************
*************************************************************
*************************************************************

Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

3f9776fefb4b452a97f24c013196c263

This may also be found at: /var/jenkins_home/secrets/initialAdminPassword

*************************************************************
*************************************************************
*************************************************************

Nov 30, 2017 10:27:12 AM hudson.model.UpdateSite updateData
INFO: Obtained the latest update center data file for UpdateSource default
--> setting agent port for jnlp
Nov 30, 2017 10:27:12 AM hudson.model.UpdateSite updateData
INFO: Obtained the latest update center data file for UpdateSource default
--> setting agent port for jnlp... done
Nov 30, 2017 10:27:13 AM hudson.WebAppMain$3 run
INFO: Jenkins is fully up and running
Nov 30, 2017 10:27:15 AM hudson.model.DownloadService$Downloadable load
INFO: Obtained the updated data file for hudson.tasks.Maven.MavenInstaller
Nov 30, 2017 10:27:18 AM hudson.model.DownloadService$Downloadable load
INFO: Obtained the updated data file for hudson.plugins.gradle.GradleInstaller
Nov 30, 2017 10:27:41 AM hudson.model.DownloadService$Downloadable load
INFO: Obtained the updated data file for hudson.tools.JDKInstaller
Nov 30, 2017 10:27:41 AM hudson.model.AsyncPeriodicWork$1 run
INFO: Finished Download metadata. 39,669 ms

# Accessing DEMOS
yum install util-linux
nsenter [containerid] 


[root@iZ2zej17ifxfecej0wo0moZ tools]# docker ps -l
CONTAINER ID        IMAGE                COMMAND                  CREATED             STATUS                     PORTS               NAMES
49f034ff2840        jenkins_24_android   "/bin/tini -- /usr..."   6 hours ago         Exited (143) 4 hours ago                       jenkins_24_android
[root@iZ2zej17ifxfecej0wo0moZ tools]# docker start 49f034ff2840
49f034ff2840
[root@iZ2zej17ifxfecej0wo0moZ tools]# docker inspect --format "{{.State.Pid}}" jenkins_24_android
28730
[root@iZ2zej17ifxfecej0wo0moZ tools]# nsenter --target 28730 --mount --uts --ipc --net --pid
mesg: ttyname failed: No such file or directory
root@49f034ff2840:/# ls
bin  boot  dev	docker-java-home  etc  home  lib  lib64  media	mnt  opt  proc	root  run  sbin  srv  sys  tmp	usr  var
root@49f034ff2840:/# 


ssh-keygen -t rsa -C "wushuifang@luojilab.com  sufun-jk" -b 4096


#in_jk_docker.sh
docker start 49f034ff2840
mpid=$(docker inspect --format "{{.State.Pid}}" jenkins_24_android)
nsenter --target $mpid --mount --uts --ipc --net --pid









