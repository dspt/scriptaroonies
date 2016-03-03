# lotsofcontainers

This is a script to build out personalized Dockerfiles for use with
docker-compose.  Originally written for DevOpsDaycamp https://devopsbootcamp.osuosl.org/daycamp/
the idea is that you have a base image, the Dockerfile, that you would like to
customize for n different people.  In this case we just want different usernames,
passwords, and ports designated for individual HTTP and SSH access.

The Dockerfile declares the set of packages and there is an array inside 
makecontainers.py which declares the usernames.

## Usage
First clone the repo and install ``docker`` and ``docker-compose``.
Then run the following commands:
(**Note**: The following code assumes your user can run docker without the need for sudo.)
```
$ cd scriptaroonies/docker/lotsofcontainers
$ ./makecontainers.py 5   # This builds 5 containers. Notice the 5 new directories!
$ docker-compose -f docker-compose.yml up    # This will build and start each of the N containers you wanted.
[... lots of docker output building the containers ...]
Creating lotsofcontainers_dugong_1...
Creating lotsofcontainers_stellarsseacow_1...
Creating lotsofcontainers_beet_1...
Creating lotsofcontainers_arrowroot_1...
Creating lotsofcontainers_manatee_1...
$ docker-compose ps    # This will check to see which containers are running and what they're doing.
              Name                       Command        State                      Ports                     
------------------------------------------------------------------------------------------------------------
lotsofcontainers_arrowroot_1        /usr/sbin/sshd -D   Up      0.0.0.0:2242->22/tcp, 0.0.0.0:8090->8080/tcp 
lotsofcontainers_beet_1             /usr/sbin/sshd -D   Up      0.0.0.0:2269->22/tcp, 0.0.0.0:8027->8080/tcp 
lotsofcontainers_dugong_1           /usr/sbin/sshd -D   Up      0.0.0.0:2283->22/tcp, 0.0.0.0:8092->8080/tcp 
lotsofcontainers_manatee_1          /usr/sbin/sshd -D   Up      0.0.0.0:2294->22/tcp, 0.0.0.0:8006->8080/tcp 
lotsofcontainers_stellarsseacow_1   /usr/sbin/sshd -D   Up      0.0.0.0:2207->22/tcp, 0.0.0.0:8081->8080/tcp
$ docker-compose -f docker-compose.yml stop    # This will stop all of the containers
Stopping lotsofcontainers_manatee_1...
Stopping lotsofcontainers_arrowroot_1...
Stopping lotsofcontainers_beet_1...
Stopping lotsofcontainers_stellarsseacow_1...
Stopping lotsofcontainers_dugong_1...
```

Hey magic!

If your containers need to have something else installed in them, edit the ``Dockerfile``
in ``scriptaroonies/docker/lotsofcontaienrs``.
