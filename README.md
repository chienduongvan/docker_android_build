# Overview
------------ 
Docker container for building android AOSP 6.x (Marshmallow) 
 
 
## Background
I have found that bleeding edge Linux distros such as Arch can have many 
issues while building android. Fixing these takes a lot of time and are not always clean. 
Therefore i have thrown together this Dockerfile to generate a container that will build 
Android without having to fix the above issues 
 
 
# Features
------------ 
 
* Based on Ubuntu 15.10 
* Downloads repo tool on build 
* Builds make 3.81 (make 4.0 has issues with build times) 
* Intended to be used with a shared volume with host 
* ccache moved to shared volume
* sudo enabled (password: build) 
 
# Usage
------------ 

*The below assumes you are working from your home directory*
 
1. Build the docker image (can take some time) 
``` 
docker build -t aosp:latest ./ 
``` 
 
2. Make your android src folder on host (this way source and out directory is available within container and on host)
``` 
mkdir aosp
``` 
 
3. Start docker container (named build with above aosp dir mounted to "/home/build/aosp") 

``` 
docker run -it -h aosp-docker --name build -v /home/$USER/aosp:/home/build/aosp aosp /bin/bash
``` 
 
4. cd into aosp directory and run normal AOSP init / sync / build
