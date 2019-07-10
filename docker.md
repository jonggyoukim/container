# docker 테스트

접속된 터미널로 다음의 명령어를 입력해 봅니다.
~~~
$ sudo docker version
$ sudo docker images
$ sudo docker ps -a
~~~

sudo 를 붙이지 않기 위해서는 opc 유저가 docker 그룹에 속하면 됩니다.
~~~
$ sudo nano /etc/group
~~~

하위 부분에 다음과 같이 있습니다.
~~~
cgred:x:994:
oracle-cloud-agent:x:993:
opc:x:1000:
docker:x:992:
~~~

맨 아래부분을 다음과 같이 opc를 추가해 줍니다.
~~~
docker:x:992:opc
~~~

F3 키를 누르거나 Ctrl-O 키를 눌러 저장합니다.<br>
F2 키를 누르거나 Ctrl-X 키를 눌러 종료합니다.



# docker search

docker search는 docker.com 에서 제공하는 이미지들을 검색하는 명령어다.  
웹브라우저에서 검색하는 방법이 훨씬 자세하고 간편하나 웹브라우저를 수행하지 못하는 환경에서 사용할 수 있는 명령어이다.

만약 mysql 이미지를 수행하려고 검색하려고 한다면 다음과 같이한다.
~~~
$ docker search mysql
NAME                                                   DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
mysql                                                  MySQL is a widely used, open-source relation…   8123                [OK]                
mariadb                                                MariaDB is a community-developed fork of MyS…   2761                [OK]                
mysql/mysql-server                                     Optimized MySQL Server Docker images. Create…   607                                     [OK]
zabbix/zabbix-server-mysql                             Zabbix Server with MySQL database support       192                                     [OK]
hypriot/rpi-mysql                                      RPi-compatible Docker Image with Mysql          113                                     
zabbix/zabbix-web-nginx-mysql                          Zabbix frontend based on Nginx web-server wi…   101                                     [OK]
centurylink/mysql                                      Image containing mysql. Optimized to be link…   60                                      [OK]
centos/mysql-57-centos7                                MySQL 5.7 SQL database server                   52                                      
1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5   ubuntu-16-nginx-php-phpmyadmin-mysql-5          50                                      [OK]
mysql/mysql-cluster                                    Experimental MySQL Cluster Docker images. Cr…   44                                      
tutum/mysql                                            Base docker image to run a MySQL database se…   31                                      
zabbix/zabbix-web-apache-mysql                         Zabbix frontend based on Apache web-server w…   29                                      [OK]
schickling/mysql-backup-s3                             Backup MySQL to S3 (supports periodic backup…   26                                      [OK]
bitnami/mysql                                          Bitnami MySQL Docker Image                      26                                      [OK]
zabbix/zabbix-proxy-mysql                              Zabbix proxy with MySQL database support        22                                      [OK]
linuxserver/mysql                                      A Mysql container, brought to you by LinuxSe…   20                                      
centos/mysql-56-centos7                                MySQL 5.6 SQL database server                   13                                      
mysql/mysql-router                                     MySQL Router provides transparent routing be…   11                                      
circleci/mysql                                         MySQL is a widely used, open-source relation…   11                                      
openshift/mysql-55-centos7                             DEPRECATED: A Centos7 based MySQL v5.5 image…   6                                       
dsteinkopf/backup-all-mysql                            backup all DBs in a mysql server                6                                       [OK]
jelastic/mysql                                         An image of the MySQL database server mainta…   1                                       
ansibleplaybookbundle/mysql-apb                        An APB which deploys RHSCL MySQL                0                                       [OK]
cloudposse/mysql                                       Improved `mysql` service with support for `m…   0                                       [OK]
widdpim/mysql-client                                   Dockerized MySQL Client (5.7) including Curl…   0                                       [OK]
~~~

웹브라우저에서 검색하면 다음과 같이 결과가 나온다.

![](https://github.com/shiftyou/cloudnative/blob/master/images/docker4.png?raw=true?raw=true)


# docker run

**docker run**은 docker image를 수행하는 명령어이다.  

hello-world 이미지를 수행해 보자.
~~~
$ docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete 
Digest: sha256:5f179596a7335398b805f036f7e8561b6f0e32cd30a32f5e19d17a3cda6cc33d
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
~~~

처음 로컬에 이미지가 존재하지 않기 때문에 이미지를 pulling 한다는 메시지가 나오고 pulling이 완료한 다음 실행한다.

httpd 를 수행해 보자.  
httpd 이미지는 Apache 그룹에서 제공하는 공식 httpd 이미지이다.

~~~
$ docker run httpd

Unable to find image 'httpd:latest' locally
latest: Pulling from library/httpd
743f2d6c1f65: Pull complete 
c92eb69846a6: Pull complete 
2211b052800a: Pull complete 
aed180197314: Pull complete 
7c472a4980a7: Pull complete 
Digest: sha256:a35ad614c1ffc6fe931f12dc42b682edbdcc62cf78d8edc41499dd90ef0f8003
Status: Downloaded newer image for httpd:latest
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
[Sat May 11 08:41:51.771929 2019] [mpm_event:notice] [pid 1:tid 139803237498944] AH00489: Apache/2.4.39 (Unix) configured -- resuming normal operations
[Sat May 11 08:41:51.772109 2019] [core:notice] [pid 1:tid 139803237498944] AH00094: Command line: 'httpd -D FOREGROUND'
~~~

hello-world 와 마찬가지로 이미지를 pulling 한다.  
이번에는 5개의 이미지를 pulling 하는 것을 볼 수 있다. 이것은 도커 이미지가 레이어로 되어있어 각 레이어를 pulling 한 것이다.
하지만, 접속을 몇번포트로 해야 하는지 알 수 없다. 그래서 일단, Ctrl-C 를 눌러 중지한다.

httpd 이미지를 사용하는 방법에 내용은 다음과 같이 되어있다.  

![](https://github.com/shiftyou/cloudnative/blob/master/images/docker5.png?raw=true)

httpd의 기본 포트는 80 이다.  
80 포트로 httpd가 서비스를 하고 있지만, 컨테이너 내에서 80으로 서비스가 되고 있어 접근이 불가능하다.  
로컬머신에서 접속하기 위해서는 포트를 호스트로 퍼블리쉬 해 주어야 한다.

Dockerfile을 사용하지 않고 수행하려면 다음과 같이 해야 한다고 되어있다.

~~~
$ docker run -dit --name my-apache-app -p 8000:80 -v "$PWD":/usr/local/apache2/htdocs/ httpd:2.4
~~~

몇가지 옵션이 사용되었는데 옵션에 docker run 명령어의 옵션을 보려면 다음과 같이 명령한다.

~~~
$ docker run --help

Usage:	docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Run a command in a new container

Options:
...
  -d, --detach                         Run container in background and print container ID
      --name string                    Assign a name to the container
  -p, --publish list                   Publish a container's port(s) to the host
  -v, --volume list                    Bind mount a volume
...
~~~

상당히 많은 옵션이 존재함을 알 수 있다. 그 중 위에서 사용한 3가지 옵션은 다음과 같다.
- -d : 컨테이너를 백그라운드로 수행
- --name : 컨테이너의 이름을 지정 (지정하지 않으면 랜덤한 이름이 기본으로 포함)
- -p : 컨테이너의 포트를 호스트로 퍼블리쉬
- -v : 볼륨 마운트

그래서 다음과 같이 httpd 를 수행한다.
~~~
$ docker run --name myhttpd -p 9090:80 httpd

AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
[Sat May 11 09:22:25.513172 2019] [mpm_event:notice] [pid 1:tid 140131185029184] AH00489: Apache/2.4.39 (Unix) configured -- resuming normal operations
[Sat May 11 09:22:25.513356 2019] [core:notice] [pid 1:tid 140131185029184] AH00094: Command line: 'httpd -D FOREGROUND'
~~~

터미널을 하나 더 열어 curl을 통해서 접속해 본다.
~~~
$ curl localhost:9090
<html><body><h1>It works!</h1></body></html>
~~~

# docker ps

현재 컨테이너들의 상태를 보는 명령어이다.
~~~
$ docker ps 

CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
0bc10989ef2b        httpd               "httpd-foreground"   About an hour ago   Up About an hour    0.0.0.0:9090->80/tcp   myhttpd
~~~

앞에서 실행했던 httpd 이미지를 사용한 myhttpd 라는 컨테이너가 수행중이다. 포트는 9090이며 컨테이너의 80포트로 포워딩 되고 있음을 보여준다.

현재 수행중인 컨테이너 뿐만 아니라 지금 수행중이지 않고 stop된 컨테이너도 보려면 -a 옵션을 사용한다
~~~
$ docker ps -a

CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS                      PORTS                  NAMES
0bc10989ef2b        httpd                           "httpd-foreground"       About an hour ago   Up About an hour            0.0.0.0:9090->80/tcp   myhttpd
8738b1ac1fee        httpd                           "-p 8080:8080"           2 hours ago         Created                     80/tcp                 distracted_perlman
d4206ffdd513        httpd                           "httpd-foreground"       2 hours ago         Exited (0) 2 hours ago                             relaxed_taussig
27e3d18d18b8        hello-world                     "/hello"                 2 hours ago         Exited (0) 2 hours ago                             wizardly_agnesi
e644b60f2da2        eb516548c180                    "/coredns -conf /etc…"   30 hours ago        Exited (1) 30 hours ago                            k8s_coredns_coredns-fb8b8dccf-x85pq_kube-system_b6f3fa60-7279-11e9-a699-08002706c4b0_17
74c664d2aa90        4689081edb10                    "/storage-provisioner"   30 hours ago        Exited (2) 30 hours ago                            k8s_storage-provisioner_storage-provisioner_kube-system_baadb436-7279-11e9-a699-08002706c4b0_2
97775652abfd        eb516548c180                    "/coredns -conf /etc…"   30 hours ago        Exited (1) 30 hours ago                            k8s_POD_etcd-minikube_kube-system_27e2185ad1fe3cab5483ad2bcc420391_0
(..중간생략..)
1449b4b8359f        k8s.gcr.io/pause:3.1            "/pause"                 42 hours ago        Exited (255) 32 hours ago                          k8s_POD_kube-apiserver-minikube_kube-system_add89b0db1b1b2ac3027599ac7fa8e44_0
a061f098969d        k8s.gcr.io/pause:3.1            "/pause"                 42 hours ago        Exited (255) 32 hours ago                          k8s_POD_kube-addon-manager-minikube_kube-system_0abcb7a1f0c9c0ebc9ec348ffdfb220c_0
~~~
위와 같이 현재 수행중이지는 않지만 생성된 컨테이너들의 리스트를 보여준다.  이러한 컨테이너는 다시 재시작할 수 있다.

# docker rm

**docker ps**로 확인한 컨테이너를 삭제하는 명령어이다.

~~~
$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
0bc10989ef2b        httpd               "httpd-foreground"   About an hour ago   Up About an hour    0.0.0.0:9090->80/tcp   myhttpd
~~~

현재 컨테이너ID 는 `0bc10989ef2b` 이고 컨테이너NAME은 `myhttpd`이다.
컨테이너를 삭제하기 위해서는 위의 두가지를 사용해서 삭제할 수 있다.
- docker rm {컨테이너ID}
- docker rm {컨테이너NAME}

그러나 현재 running중인 컨테이너이기 때문에 삭제를 하면 다음과 같은 오류가 난다.
~~~
$ docker rm 0bc10989ef2b
Error response from daemon: You cannot remove a running container 0bc10989ef2b4457c2ea6a8d9ac97271c4051430dfc57c3e2b111ec6a5853c1c. Stop the container before attempting removal or force remove

$ docker rm myhttpd
Error response from daemon: You cannot remove a running container 0bc10989ef2b4457c2ea6a8d9ac97271c4051430dfc57c3e2b111ec6a5853c1c. Stop the container before attempting removal or force remove
~~~

그래서 먼저 컨테이너를 중지하고 rm 명령을 내리면 삭제가 가능하다.

# docker stop

컨테이너를 중지하는 명령어이다.  
앞서 설명한 rm 과 동일한 방법으로 컨테이너 중지가 가능하다.
- docker stop {컨테이너ID}
- docker stop {컨테이너NAME}

다음과 같이 컨테이너를 중지해본다.
~~~
$ docker ps

CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
0bc10989ef2b        httpd               "httpd-foreground"   About an hour ago   Up About an hour    0.0.0.0:9090->80/tcp   myhttpd

$ docker stop myhttpd
myhttpd

$ docker ps -a | grep myhttpd
0bc10989ef2b        httpd                           "httpd-foreground"       About an hour ago   Exited (0) 3 minutes ago                        myhttpd
~~~
수행중이던 myhttpd 가 중지됨을 알 수 있다.

이후 `docker rm`명령을 하면 컨테이너를 삭제할 수 있다.
~~~
$ docker ps -a | grep myhttpd
0bc10989ef2b        httpd                           "httpd-foreground"       About an hour ago   Exited (0) 3 minutes ago                        myhttpd

$ docker rm myhttpd
myhttpd

$ docker ps -a | grep myhttpd
(삭제되어 아무것도 나오지 않는다) 
~~~


# docker start

STOP 된 컨테이너를 다시 재시작하는 명령어이다.
stop 과 마찬가지로 컨테이너ID 및 컨테이너NAME으로 시작할 수 있다.
- docker start {컨테이너ID}
- docker start {컨테이너NAME}

~~~
$ docker start 0bc10989ef2b
$ docker start myhttpd
~~~


# docker images

컨터이너를 수행하기 위해서는 이미지가 있어야 한다. docker image registry에서 pulling한 이미지들은 다음과 같이 볼 수 있다.
~~~
$ docker images

REPOSITORY                                TAG                 IMAGE ID            CREATED             SIZE
httpd                                     latest              b7cc370ac278        3 days ago          132MB
k8s.gcr.io/kube-proxy                     v1.14.1             20a2d7035165        4 weeks ago         82.1MB
k8s.gcr.io/kube-apiserver                 v1.14.1             cfaa4ad74c37        4 weeks ago         210MB
k8s.gcr.io/kube-controller-manager        v1.14.1             efb3887b411d        4 weeks ago         158MB
k8s.gcr.io/kube-scheduler                 v1.14.1             8931473d5bdb        4 weeks ago         81.6MB
k8s.gcr.io/kube-addon-manager             v9.0                119701e77cbc        3 months ago        83.1MB
k8s.gcr.io/coredns                        1.3.1               eb516548c180        3 months ago        40.3MB
hello-world                               latest              fce289e99eb9        4 months ago        1.84kB
k8s.gcr.io/etcd                           3.3.10              2c4adeb21b4f        5 months ago        258MB
k8s.gcr.io/pause                          3.1                 da86e6ba6ca1        16 months ago       742kB
gcr.io/k8s-minikube/storage-provisioner   v1.8.1              4689081edb10        18 months ago       80.8MB
node                                      6.3                 0d9089853221        2 years ago         651MB
~~~
현재 다음에 설명할 Kubernetes에 대한 이미지와 처음에 수행한 hello-world 이미지, 그리고 httpd 이미지 등이 존재한다.

# docker rmi

다운로드 받은 이미지를 로컬 디스크에서 삭제하는 명령이다. 
~~~
$ docker rmi httpd

Untagged: httpd:latest
Untagged: httpd@sha256:a35ad614c1ffc6fe931f12dc42b682edbdcc62cf78d8edc41499dd90ef0f8003
Deleted: sha256:b7cc370ac278cb8b059c2de708b4a687e079919779da32a6682bc73dc9398d87
Deleted: sha256:6933e5c4e029ac60cd7a6a3fbf10bd947f8a0f3fa8642b5ee8d9a9bf941673c8
Deleted: sha256:0f1c16bb6491fbc5f56b7b76bab8690ee6fbb497bdb691a5cf226d368d47ca4b
Deleted: sha256:cf5f6dc294d6ab63edad7d34107dc1f05e2fed66919c3444d92555624c1be25f
Deleted: sha256:6fb6246d14e214ead4424482b2c53059e7e2a82c2d9fa8aa3a9ef4d574051e29
Deleted: sha256:6270adb5794c6987109e54af00ab456977c5d5cc6f1bc52c1ce58d32ec0f15f4
~~~

컨테이너 이미지가 레이어로 되어 있기 때문에 해당 레이어 모두를 삭제하는 과정이 나타난다.

컨테이너 이미지는 하나이지만 실제로 수행되는 컨테이너는 여러개 있을 수 있다. 그래서 현재 수행되지 않고 STOP된 컨테이너가 존재한다면 이미지를 삭제할 때 다음과 같은 메시지가 나온다.
~~~
Error response from daemon: conflict: unable to remove repository reference "httpd" (must force) - container 8738b1ac1fee is using its referenced image b7cc370ac278
~~~

위와같은 메시지가 나오면 `docker ps -a | grep {이미지명}`로 현재 로드된 컨테이너들을 살펴보고 해당 컨테이너를 삭제한 후 이미지를 삭제할 수 있다.


# docker exec

컨테이너 안의 실행파일을 수행하는 명령어이다.
mysql을 컨테이너로 시작하고, sql을 수행하기 위해서 다음과 같이 할 수 있다.

mysql은 docker.com에서 살펴보면 다음과 같다.

![](https://github.com/shiftyou/cloudnative/blob/master/images/docker8.png?raw=true)

mysql 컨테이너의 실행은 다음과 같이 한다.
~~~
$ docker run --name mydb -e MYSQL_ROOT_PASSWORD=mypassword -d mysql:5

Unable to find image 'mysql:5' locally
5: Pulling from library/mysql
743f2d6c1f65: Already exists 
3f0c413ee255: Pull complete 
aef1ef8f1aac: Pull complete 
f9ee573e34cb: Pull complete 
3f237e01f153: Pull complete 
f9da32e8682a: Pull complete 
4b8da52fb357: Pull complete 
6f38e9cfd49b: Pull complete 
9f4834b3f44f: Pull complete 
af631d92fdba: Pull complete 
0e771ddab25c: Pull complete 
Digest: sha256:196fe3e00d68b2417a8cf13482bdab1fcc2b32cf7c7575d0906c700688b352b4
Status: Downloaded newer image for mysql:5
574e3cb58480994e6995edd2ead4b6a6daa8b624b5b4f435502e4c853a0e91c0
~~~

잘 실행되고 있는지 살펴본다.

~~~
$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
574e3cb58480        mysql:5             "docker-entrypoint.s…"   2 minutes ago       Up 2 minutes        3306/tcp, 33060/tcp   mydb
~~~

컨테이너에 접속하기 위해서 다음과같이 수행한다.

~~~
$ docker exec -it {컨테이너명} {명령어}
~~~

- -i: interactive라는 뜻으로, 컨테이너와 상호적으로 주고받고 하겠다는 뜻
- -t: tty라는 뜻으로 tty를 사용하겠다는 뜻이다. (합해서 -it 로 옵션을 준다)

~~~
$ docker exec -it mydb bash

root@574e3cb58480:/# ls
bin  boot  dev	docker-entrypoint-initdb.d  entrypoint.sh  etc	home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

root@574e3cb58480:/# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.7.26 MySQL Community Server (GPL)

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
~~~

위와같이 컨테이너 내부의 명령어를 실행 할 수 있다.


# DockerFile 설명

지금까지는 이미 만들어져 있는 이미지를 사용하였다.
이번에는 나만의 새로운 이미지를 만드는 작업이다.

애플리케이션을 만들거나 나만을 위한 설정이 담긴 이미지를 만들기 위해서 Dockerfile을 만든다.
Dockerfile은 docker image를 만들기 위한 설정파일이다.  
아래는 아주 짧은 Dockerfile의 예이다.

~~~dockerfile
FROM busybox
CMD echo "hello world"
~~~

각 라인의 의미는 다음과 같다.

- 
    ~~~dockerfile
    FROM busybox
    ~~~
    busybox는 리눅스의 명령어들을 담고있는 작은 리눅스이미지이다.  
    busybox 이미지를 토대로 새로운 이미지를 만든다는 의미이다.
    
- 
    ~~~dockerfile
    CMD echo "hello world"
    ~~~
    현재의 레이어에서 "hello world" 라는 문구를 출력해라는 의미이다


다음은 다른 Dockerfile의 예제이다.

~~~dockerfile
from node:alpine
run mkdir -p /usr/src/app
workdir /usr/src/app
copy package*.json ./
run npm install
copy . .
expose 8080
cmd ["npm", "start"] 
~~~
위의 도커파일의 내용을 설명하면,
1. node 이미지 8 태그를 기반으로  
1. /usr/src/app 디렉토리를 만들고
1. /usr/src/app 로 현재디렉토리를 옮기고
1. 로컬 디렉토리의 package*.json 파일을 컨테이너로 복사를 하고
1. npm install 명령을 새로운 레이어를 통해서 수행하고
1. 현재 디렉토리의 모든 파일을 컨테이너로 복사를 하고
1. 8080 포트를 열어주고
1. npm start 명령을 내린다.

이다.

위와같이 Dockerfile 안에는 어떤 이미지를 기본으로 어떠한 변화를 줄 것이고 어떤 명령을 할 것인가를 담고 있다.  
이젠 이 Dockerfile로 이미지를 만들 차례이다.

# docker build

Dockerfile로 부터 docker image 를 만드는 명령어이다.

~~~dockerfile
FROM busybox
CMD echo "hello world"
~~~

위의  Dockerfile을 사용하여 hello라는 이름의 image를 만들어 보자.

~~~
$ docker build -t hello .

Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM busybox
 ---> 64f5d945efcc
Step 2/2 : CMD echo "hello world"
 ---> Running in 28821954a278
Removing intermediate container 28821954a278
 ---> d9bb3b6b58bf
Successfully built d9bb3b6b58bf
Successfully tagged hello:latest
~~~

실제로 잘 만들어졌는지 docker image로 살펴본다.
~~~
$ docker images hello
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
hello               latest              d9bb3b6b58bf        About a minute ago   1.2MB
~~~

만든 이미지로 컨테이너를 실행한다.
~~~
$ docker run --name hello hello
hello world
~~~

컨테이너에서 hello world 출력이 잘 됨을 알 수 있다.

# docker logs
컨테이너의 로그를 보는 명령어이다. 컨테이너에서 Stdout/Stderr으로 보내진 메시지를 다시 볼 수 있다.  
기존에 실행했던 hello 컨테이너에 대해서 명령을 내려본다.
~~~
$ docker logs hello 
hello world
~~~
정상적으로 로그를 볼 수 있다.

기존에 수행했던 httpd 컨테이너를 삭제하지 않았다면 다음과 같이 볼 수 있다.
~~~
$ docker logs myhttpd

AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
[Sat May 11 11:13:55.154044 2019] [mpm_event:notice] [pid 1:tid 140534610489408] AH00489: Apache/2.4.39 (Unix) configured -- resuming normal operations
[Sat May 11 11:13:55.154195 2019] [core:notice] [pid 1:tid 140534610489408] AH00094: Command line: 'httpd -D FOREGROUND'
[Sat May 11 11:14:07.398350 2019] [mpm_event:notice] [pid 1:tid 140534610489408] AH00491: caught SIGTERM, shutting down
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
[Sat May 11 11:14:14.522862 2019] [mpm_event:notice] [pid 1:tid 140437646258240] AH00489: Apache/2.4.39 (Unix) configured -- resuming normal operations
[Sat May 11 11:14:14.523001 2019] [core:notice] [pid 1:tid 140437646258240] AH00094: Command line: 'httpd -D FOREGROUND'
~~~

컨테이너에서 발생하는 로그나 오류메시지를 볼 때 사용된다.


# docker.com 계정 만들기

docker를 사용하기 위해서는 docker image registry에서 docker image를 다운로드받고, 자신의 이미지를 docker registry에 업로드 할 수 있어야 한다. 다운로드는 계정을 만들 필요는 없지만, 업로드를 위해서는 docker.com 에서 제공하는 docker image resistry를 사용하기 위하여 계정을 만들어야 한다.

1. hub.docker.com 에 접속한다.

    웹브라우저로 hub.docker.com 에 접속을 한다. hub.docker.com 은 docker 사에서 제공하는 public docker image registry이다.

    ![](https://github.com/shiftyou/cloudnative/blob/master/images/docker1.png?raw=true)

    "sign up for Docker Hub"를 선택하여 계정을 만든다.

    등록한 email을 통하여 인증을 하면 다음과 같이 로그인된다.

    ![](https://github.com/shiftyou/cloudnative/blob/master/images/docker2.png?raw=true)

    이제 자신만의 docker image registry가 생겼다.

# docker login

로컬머신에 docker가 설치되었으면 docker image registry에 접근 하기위하여 docker login 을 한다.
~~~
$ docker login

Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: <username. not email>
Password: <password>
WARNING! Your password will be stored unencrypted in /home/user1/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
~~~
로그인을 완료함으로 docker image registry에 docker image 업로드가 가능하다.


# hello 이미지 만들어서 레지스트리에 올리기

hello 디렉토리를 만들고 node.js 로 동작하는 샘플을 만들어 보도록 한다.

~~~
$ mkdir hello
$ cd hello
~~~

server.js
~~~
var http = require('http');
var os = require('os');

var handleRequest = function(request, response) {
  console.log('Received request for URL: ' + request.url);
  response.writeHead(200);
  response.end('Hello World!' + os.hostname());
};
var www = http.createServer(handleRequest);
www.listen(8000);
console.log(os.hostname() + " Server listening..");
~~~

Dockerfile
~~~
FROM node:slim
EXPOSE 8000
COPY server.js .
CMD node server.js
~~~

hello 이미지를 만든다. (개인의 docker hub 아이디를 쓴다.)
~~~
$ docker build -t {docker.com username}/hello .

or

$ docker build -t {docker.com username}/hello -f Dockerfile .
~~~

레지스트리 등록한다. (push가 되지 않으면 로그인을 먼저 한다)
~~~
$ docker push {docker.com username}/hello
~~~
