# Docker-cmd
``Author: HackBugs``

### Docker
- `sudo systemctl status docker`
- `sudo systemctl restart docker`
- `sudo systemctl start docker`

### Dockerfile
 --docker image
     ---docker containers
     ---docker containers
     ---docker containers
     ---docker containers

  - docker version
  - docker --version
  - docker compose version

  - docker run -p 80:80 nginx  --map prot container machine to primary machine

  - docker system prune --
  - docker system prune --

  - docker pull nginx -- this cmd like "git clone" show only image section not in container section
  - dcoekr run nginx -- this cmd use to meke image to build container and show container section

  - docker search mysql --know information about particular package
  - docker history nginx --know history of particular package
  - docker logs nginx --can check logs of particular container
  - docker ps -a | grep nginx

  - dcoker images
  - dcoker ps -a

  - docker pull "image-name" --downlaod the container from docker hub
  - docker run "image-name" --This cmd will install and run the image togethr the
  - docker run -it "image-name" -- with this cmd we can install image and run and also will enter inside/into container

  - docker run --name "image-name" --can duplicate the image
  - Ex- docker run --name nginx-2nd  nginx

  - docker run --name nginx-2nd -it -d nginx

  - docker run -it alpine
  - docker exec alpine -d -it alpine /bin/sh
  - --if i want to run in background, of any container than i use -d

  - docker inspect "container_id" --to this cmd you can inspect of any container and can know all the information of container.

  - docker push nginx  --thix cmd like use "git push origin main"

  - ------------------------------------------------------------------

  - docker pull mysql
  - docker run --name mysql-c1 -e MYSQL_ROOT_PASSWORD=@#123 -d mysql
  - docker exec -it mysql-c1 mysql -u root -p


  - docker run --name phpmyadmin-c1 -d -p 8080:80 -v /mnt/c/my-website/index.html:/var/www/html/index.html phpmyadmin

  - docker run -d -p 8001:80 --name phpmyadmin-c3 phpmyadmin

  - ----------------------------------------------------------------

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
