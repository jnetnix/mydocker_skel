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
