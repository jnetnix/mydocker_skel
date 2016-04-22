#Docker Skeleton
The Docker Skeleton is a way to dockerize your applications. 

#Get the files local
```
git clone https://github.com/jnetnix/mydocker_skel.git
```

#Put them into your new project folder.
```
rsync \
  -a \
  --verbose \
  --stats \
  --exclude ".git" \
./mydocker_skel/* \
~/workspace/<new_project>
```

#Handling your new container.
Now, modify it to fit the needs of your APP.
```
cd ~/workspace/<new_project>

#Buld an Image
./ctrl/buildit;

#Attach to that Image
./ctrl/attachit;

#Just run the image (looks for run.sh)
./ctrl/runit_new;
```

#Example Run

##Clone the Skeleton
```
bash-3.2$ git clone https://github.com/jnetnix/mydocker_skel.git
Cloning into 'mydocker_skel'...
remote: Counting objects: 30, done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 30 (delta 5), reused 25 (delta 3), pack-reused 0
Unpacking objects: 100% (30/30), done.
Checking connectivity... done.
bash-3.2$ 
```

##Rsync the Skeleton into Your New Project Directory.
```
bash-3.2$ mkdir mydocker_skel_test
bash-3.2$ rsync \
>   -a \
>   --verbose \
>   --stats \
>   --exclude ".git" \
> ./mydocker_skel/* \
> ~/workspace/mydocker_skel_test/
building file list ... done
Dockerfile_Base
LICENSE
README.md
app/
app/bin/
app/bin/.keep
app/bin/run.sh
app/etc/
app/etc/.keep
app/etc/banner.txt
app/lib/
app/lib/.keep
app/var/
app/var/.keep
ctrl/
ctrl/attachit
ctrl/buildit
ctrl/runit_new
local_config/
local_config/env.sh

Number of files: 20
Number of files transferred: 13
Total file size: 39285 bytes
Total transferred file size: 39285 bytes
Literal data: 39285 bytes
Matched data: 0 bytes
File list size: 365
File list generation time: 0.004 seconds
File list transfer time: 0.000 seconds
Total bytes sent: 40294
Total bytes received: 348

sent 40294 bytes  received 348 bytes  81284.00 bytes/sec
total size is 39285  speedup is 0.97
```

##Build your Container.
```
bash-3.2$ cd ./mydocker_skel_test/
bash-3.2$ ./ctrl/buildit 
Building a New docker_skel Container for jhilving.
Sending build context to Docker daemon 54.27 kB
Step 1 : FROM ubuntu
 ---> c88b54fedc4f
Step 2 : RUN apt-get update --fix-missing ;     apt-get -y install unzip
rsync wget
 ---> Using cache
 ---> 7f65395dffe2
Step 3 : COPY app/ /opt/docker_skel/
 ---> 207626d87659
Removing intermediate container 21c52acebc04
Step 4 : RUN cat /opt/docker_skel/etc/banner.txt >> /etc/motd ;     echo
"cat /etc/motd" >> /etc/profile
 ---> Running in 353ee56ea976
 ---> 6577bc4f3f91
Removing intermediate container 353ee56ea976
Step 5 : WORKDIR /opt/docker_skel/bin/
 ---> Running in edcfbf652347
 ---> 95c8c1dc3990
Removing intermediate container edcfbf652347
Step 6 : CMD bash --login
 ---> Running in 7b556fc3ee4c
 ---> 7c55ae9e01da
Removing intermediate container 7b556fc3ee4c
Successfully built 7c55ae9e01da
Build Local Image - docker_skel
Sending build context to Docker daemon 54.27 kB
Step 1 : FROM ubuntu
 ---> c88b54fedc4f
Step 2 : RUN apt-get update --fix-missing ;     apt-get -y install unzip
rsync wget
 ---> Using cache
 ---> 7f65395dffe2
Step 3 : COPY app/ /opt/docker_skel/
 ---> Using cache
 ---> 207626d87659
Step 4 : RUN cat /opt/docker_skel/etc/banner.txt >> /etc/motd ;     echo
"cat /etc/motd" >> /etc/profile
 ---> Using cache
 ---> 6577bc4f3f91
Step 5 : WORKDIR /opt/docker_skel/bin/
 ---> Using cache
 ---> 95c8c1dc3990
Step 6 : CMD bash --login
 ---> Using cache
 ---> 7c55ae9e01da
Successfully built 7c55ae9e01da
bash-3.2$ 
```

##Connect to your new container.
bash-3.2$ ./ctrl/attachit 
Entering a New docker_skel Container for jhilving. Exit will destroy
Container.
Run Local Image
---------------------------------------------------------------------------------------
 __  __         _____             _                _____ _        _ 
|  \/  |       |  __ \           | |              / ____| |      | |
| \  / |_   _  | |  | | ___   ___| | _____ _ __  | (___ | | _____| |
| |\/| | | | | | |  | |/ _ \ / __| |/ / _ \ '__|  \___ \| |/ / _ \ |
| |  | | |_| | | |__| | (_) | (__|   <  __/ |     ____) |   <  __/ |
|_|  |_|\__, | |_____/ \___/ \___|_|\_\___|_|    |_____/|_|\_\___|_|
         __/ |                                                      
        |___/                                                       

#TODO: Modify the Banner to meet your App..

History:
  2016/04/21 - Shared My Docker Skel with github. j.hilving
               https://github.com/jnetnix/mydocker_skel.git
root@docker_skel:/opt/docker_skel/bin# 
```

##Next Steps
```
root@docker_skel:/opt/docker_skel/bin# ./run.sh 

  Welcome to the Docker Skeleton!
  Todo:
    - Modify the <base>/app/ location to have the files you care about. 
    - modify the Dockerfile_base to do whatever is needed for your
      container.
    - Tweak the ./ctrl/ if need be. 
    - Run ./ctr/buildit to build a container. 
    - Run ./ctrl/buildit dreg to send it to send it to you Docer
      Repository.
    - Run ./ctrl/attachit to get insire.
    - Run ./ctrl/runnew to just run the run.sh here.
```
