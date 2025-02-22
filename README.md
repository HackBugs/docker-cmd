# Docker-cmd ✅
``Author: HackBugs``

```sh
docker logout
docker login

cmd - docker run -td --name port-sharing -p 80:80 ubuntu
cmd - docker port port-sharing
cmd - docker exec -it port-sharing /bin/bash
cmd - apt-get update
cmd - apt-get install apache2 -y
cmd - cd /var/www/html
cmd - echo "Hello i installed apache2 on my dcoker" >index.html
cmd - service apache2 restart
Paste this URL on your browser - http://127.0.0.1 - http://localhost

cmd - docker run -td --name myjenkins -p 8080:8080 jenkins/jenkins:lts
http://localhost:8080

Docker File
Docker Image - We can download as per aur requerement images from DockerHub
Docker Container - After downloading image form DockerHub we can run
If image is in running state we called container
We made with mutiple file docker image and image share and transfer we other people

Create container and volume and share volume to each other
docker run -it --name container3  -v /volume2 ubuntu /bin/bash
docker run -it --name container4 --privileged=true --volumes-from container3 ubuntu /bin/bash

Start container
docker start container3
docker attach container3
```

### Docker
- `sudo systemctl status docker`
- `sudo systemctl restart docker`
- `sudo systemctl start docker`
------------------------------------------------------------------
### Dockerfile
 - docker image
     - docker containers
     - docker containers
     - docker containers
     - docker containers
------------------------------------------------------------------
  - docker version
  - docker --version
  - docker compose version
------------------------------------------------------------------
  - docker run -p 80:80 nginx  --map prot container machine to primary machine
------------------------------------------------------------------
  - docker system prune --
  - docker system prune --
------------------------------------------------------------------
  - docker pull nginx -- this cmd like "git clone" show only image section not in container section
  - dcoekr run nginx -- this cmd use to meke image to build container and show container section
------------------------------------------------------------------
  - docker search mysql --know information about particular package
  - docker history nginx --know history of particular package
  - docker logs nginx --can check logs of particular container
  - docker ps -a | grep nginx
------------------------------------------------------------------
  - dcoker images
  - dcoker ps -a
------------------------------------------------------------------
  - docker pull "image-name" --downlaod the container from docker hub
  - docker run "image-name" --This cmd will install and run the image togethr the
  - docker run -it "image-name" -- with this cmd we can install image and run and also will enter inside/into container
------------------------------------------------------------------
  - docker run --name "image-name" --can duplicate the image
  - Ex- docker run --name nginx-2nd  nginx
------------------------------------------------------------------
  - docker run --name nginx-2nd -it -d nginx
------------------------------------------------------------------
  - docker run -it alpine
  - docker exec alpine -d -it alpine /bin/bash
  - --if i want to run in background, of any container than i use -d
------------------------------------------------------------------
  - docker inspect "container_id" --to this cmd you can inspect of any container and can know all the information of container.
------------------------------------------------------------------
  - docker push nginx  --thix cmd like use "git push origin main"

  - ------------------------------------------------------------------

  - docker pull mysql
  - docker run --name mysql-c1 -e MYSQL_ROOT_PASSWORD=@#123 -d mysql
  - docker exec -it mysql-c1 mysql -u root -p


  - docker run --name phpmyadmin-c1 -d -p 8080:80 -v /mnt/c/my-website/index.html:/var/www/html/index.html phpmyadmin

  - docker run -d -p 8001:80 --name phpmyadmin-c3 phpmyadmin

<hr>

> # Docker mein ek hi command se band (stopped) container ko stop aur remove karna, aur image ko delete karne ke liye aap yeh commands use kar sakte hain: ✅

### 1. **Stopped Containers Ko Stop Aur Remove Karna**:
Agar aapko **sabhi stopped containers** ko stop aur remove karna hai, toh aap yeh command use kar sakte hain:
```bash
docker container prune -f
```
Is command se sabhi stopped containers ko **forcefully** remove kar diya jayega.

### 2. **Ek Specific Stopped Container Ko Stop Aur Remove Karna**:
Agar aapko ek specific container ko stop aur remove karna hai, toh yeh commands use kar sakte hain:
- **Stop the container**:
  ```bash
  docker stop <container_id_or_name>
  ```
- **Remove the container**:
  ```bash
  docker rm <container_id_or_name>
  ```

### 3. **Docker Images Ko Delete Karna**:
#### **Ek Specific Image Ko Delete Karna**:
Agar aapko ek specific image ko delete karna hai, toh yeh command use karein:
```bash
docker rmi <image_id_or_name>
```

#### **Multiple Images Ko Ek Saath Delete Karna**:
Agar aapko multiple images ko ek saath delete karna hai, toh aap in images ke IDs ko comma-separated list mein de sakte hain:
```bash
docker rmi <image_id1> <image_id2> <image_id3>
```

#### **Sabhi Unused Images Ko Clean Karna**:
Agar aapko sabhi **unused** images ko remove karna hai, toh yeh command use karein:
```bash
docker image prune -a -f
```

Yeh command **all unused images** ko delete kar degi jo kisi running container se connected nahi hain.

### Example:
1. **Stop and remove all stopped containers**:
   ```bash
   docker container prune -f
   ```

2. **Remove a specific image**:
   ```bash
   docker rmi zabbix/zabbix-web-nginx-pgsql:latest
   ```

3. **Remove multiple images at once**:
   ```bash
   docker rmi image_id1 image_id2 image_id3
   ```

Is tarah se aap Docker mein containers aur images ko efficiently manage kar sakte hain.

<hr>

# **Check process Running on docker and laptop or linux**

   - Aapko Jenkins instance ka origin (local machine ya Docker) identify karne ke liye kuch steps follow karne padenge. Yeh steps aapko yeh samajhne mein madad karenge ki Jenkins kaha se run ho raha hai.

### Steps to Identify Jenkins Instance Origin

1. **Check Running Docker Containers:**
   Yeh ensure karne ke liye ki koi Jenkins container Docker mein run ho raha hai:
   ```sh
   docker ps
   ```

   Output kuch is tarah ka ho sakta hai:
   ```sh
   CONTAINER ID   IMAGE             COMMAND                  CREATED          STATUS                      PORTS                    NAMES
   c9b8e7a0a234   jenkins/jenkins   "/sbin/tini -- /usr/…"   2 hours ago      Up 2 hours                  0.0.0.0:8080->8080/tcp   jenkins
   ```

2. **Check Local Processes:**
   Agar Docker mein koi Jenkins container run nahi ho raha, toh check karein ki kya Jenkins local machine pe run ho raha hai. Windows pe `Task Manager`, macOS pe `Activity Monitor`, aur Linux pe `ps` command use kar sakte hain.

   Windows PowerShell:
   ```sh
   netstat -aon | findstr :8080
   ```
   Isse aapko process ID (`PID`) milegi jo port 8080 pe listen kar rahi hai.

   Linux:
   ```sh
   sudo lsof -i :8080
   ```
   Mac:
   ```sh
   lsof -i :8080
   ```

   Output example:
   ```sh
   COMMAND   PID   USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
   java      1234  user   45u  IPv6 0t0   TCP *:http-alt (LISTEN)
   ```

3. **Identify and Stop the Process:**
   Agar process ID (`PID`) mil gayi, toh us process ko terminate karein.

   Windows:
   ```sh
   taskkill /PID <PID> /F
   ```

   Linux:
   ```sh
   sudo kill -9 <PID>
   ```

4. **Verify Docker and Local Services:**
   Ensure karein ki koi Jenkins service Docker ya local machine pe run na ho rahi ho.

### Additional Commands for Docker:
1. **Stop All Running Containers:**
   ```sh
   docker stop $(docker ps -q)
   ```

2. **Remove All Containers:**
   ```sh
   docker rm $(docker ps -aq)
   ```

3. **Verify Docker Images:**
   ```sh
   docker images
   ```
   Ensure karein ki koi unwanted Jenkins image present na ho.

### Checking Jenkins Installation on Local Machine:
1. **Check Installed Services (Linux/Mac):**
   ```sh
   systemctl list-units --type=service | grep jenkins
   ```

2. **Check Installed Applications (Windows):**
   - Open `Control Panel`
   - Go to `Programs and Features`
   - Look for Jenkins in the installed programs list.

### Summary:
- **Docker:** Ensure koi Jenkins container run nahi ho raha.
- **Local Machine:** Check running processes aur installed services.

In steps ko follow karke aap identify kar sakte hain ki Jenkins kaha se run ho raha hai aur accordingly action le sakte hain.

### Push docker container to local machine 
- docker tag "image-id" "username"/"image-name"
- login "username"
- password "password"
- docker push "username"/"imagename"

### Create docker volume
- docker volume create "volume-name"
- docker volume ls --show "volume" detaila
- docker volume inspect "volume-name"

### mount into container of volume
- docker run --name "container-name" -idt -v "volume-name":/"maapp" "image-name"
--------------------------------------------------------------------------------------

### Yahaan Docker ke kuch mukhya commands aur flags ke saath unke short explanations aur examples diye gaye hain:

### Docker Commands:

1. **docker ps**
   - Lists running containers.
   ```sh
   docker ps
   ```

2. **docker ps -a**
   - Lists all containers (running and stopped).
   ```sh
   docker ps -a
   ```

3. **docker images**
   - Lists all downloaded images.
   ```sh
   docker images
   ```

4. **docker run**
   - Runs a command in a new container.
   ```sh
   docker run <image_name>
   ```

5. **docker exec**
   - Runs a command in a running container.
   ```sh
   docker exec <container_id_or_name> <command>
   ```

6. **docker stop**
   - Stops one or more running containers.
   ```sh
   docker stop <container_id_or_name>
   ```

7. **docker rm**
   - Removes one or more containers.
   ```sh
   docker rm <container_id_or_name>
   ```

8. **docker rmi**
   - Removes one or more images.
   ```sh
   docker rmi <image_id_or_name>
   ```

### Docker Flags:

1. **-it**
   - Attaches an interactive terminal to the container.
   ```sh
   docker run -it <image_name> bash
   ```

2. **-v**
   - Mounts a volume from the host system to the container.
   ```sh
   docker run -v /host/path:/container/path <image_name>
   ```

3. **-p**
   - Maps a host port to a container port.
   ```sh
   docker run -p 8080:80 <image_name>
   ```

4. **-d**
   - Runs the container in detached mode (background).
   ```sh
   docker run -d <image_name>
   ```

5. **--name**
   - Assigns a name to the container.
   ```sh
   docker run --name my-container <image_name>
   ```

6. **--rm**
   - Automatically removes the container when it exits.
   ```sh
   docker run --rm <image_name>
   ```

7. **--network**
   - Specifies the network to which the container should connect.
   ```sh
   docker run --network my-network <image_name>
   ```

8. **--link**
   - Links another container to the running container.
   ```sh
   docker run --link db-container:mysql <image_name>
   ```

### Examples:

1. **Run a MySQL container:**
   ```sh
   docker run -d --name mysql-db -e MYSQL_ROOT_PASSWORD=password mysql:latest
   ```

2. **Attach to an interactive terminal:**
   ```sh
   docker exec -it mysql-db bash
   ```

3. **Mount a volume:**
   ```sh
   docker run -v /host/data:/container/data myapp
   ```

4. **Map ports:**
   ```sh
   docker run -p 8080:80 myapp
   ```

5. **Remove a container automatically when it exits:**
   ```sh
   docker run --rm myapp
   ```

6. **Assign a name to a container:**
   ```sh
   docker run --name my-container myapp
   ```

7. **Link containers:**
   ```sh
   docker run --link mysql-db:mysql myapp
   ```

Yeh commands aur flags Docker ke basic operations ko cover karte hain. Inka use Docker containers ko manage aur interact karne mein kiya ja sakta hai.


