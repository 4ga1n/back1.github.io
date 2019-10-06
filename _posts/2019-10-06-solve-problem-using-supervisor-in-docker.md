---
layout: post
title: "Solve "unix:///var/run/supervisor.sock refused connection" when using supervisor in docker container"
category: tools
---

# Problem

I meet a problem that supervisorctl alerting "unix:///var/run/supervisor.sock refused connection" when I using it in docker container. I thought it's a supervisor problem and reinstalled it many times but the situation occured again and again. Then I thought there should be some lib that the docker image missed so I changed 5 images, but all of them were not compatiable. 

Fianlly I turn to Google and found that the overlayfs using by docker has a bug dealing with unix socket.

# Solution

Change the position of socket file to "/dev/shm/supervisor.sock". "/dev/shm/" is a folder in memory and not using overlayfs, so that will be ok for your socket file.