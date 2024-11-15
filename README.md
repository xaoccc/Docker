# Docker
Docker training

1. Run app from existing image

```docker run -it --name mycontainername -p 8080:8080 -v ${PWD}:/app -w /app node:16 npm run serve```

- Explanation of Each Part
- `docker run`: Starts a new Docker container.

- `-it`:  
`-i` (interactive) keeps the standard input open, allowing you to interact with the container.
`-t` (TTY) allocates a terminal, making the output more readable.
- `-p 8080:8080`: Maps port 8080 on your local machine (host) to port 8080 inside the container.  
- `--name`: the name of the container  
This is essential if the application inside the container serves on port 8080 and you want to access it from your browser or other tools on your local machine.  
- `-v ${PWD}:/app`: Mounts the current directory (`${PWD}`) from your local machine to the /app directory inside the container.  
${PWD} is an environment variable that represents the present working directory (i.e., the directory you're currently in).
This makes your local files accessible inside the container and allows changes you make locally to be reflected immediately in the container.  
- `-w /app`: Sets the working directory inside the container to /app.  
This means all commands will be executed from within the /app directory inside the container.  
- `node:16`: Specifies the Docker image to use, in this case, node:16.  
This image includes Node.js version 16, which allows you to run Node.js applications.  
- `npm run serve`: Command that will be executed inside the container. `npm run serve` typically starts the application (if your package.json file has a serve script defined, often used with frontend frameworks like Vue.js).

2. Create and publish docker image
- Create the Dockerfile
- Build the image: `docker image build -t my-app`  
- You can see if was created using this command: `docker images`  
- Create a repository in dockerhub or use existing one
- Tag (commit) the image: `docker tag my-website my_profile/my_repo:latest`
- Push the image into dockerhub: `docker push my_profile/my_repo:latest`


3. Creating docker network  
`docker network create my_network`  
If the above command is returning an error: `error during connect...`  
run this command `docker context use default` and try againg to create a network  


`docker run -dit  --name wordpress_app -e MYSQL_ROOT_PASSWORD=pass -e MYSQL_DATABASE=wordpressdb  -e MYSQL_USER=wordpress  -e MYSQL_PASSWORD=wordpress  --expose 3306 --expose 33060 --network my_network  -v ${PWD}/data:/var/lib/mysql  mysql`

`docker network inspect my_network`  

`docker run -dit --name wordpress-website -e WORDPRESS_DB_HOST=wordpress_app -e WORDPRESS_DB_USER=wordpress -e WORDPRESS_DB_PASSWORD=wordpress -e WORDPRESS_DB_NAME=wordpressdb -v ${PWD}/wp-data:/var/www/html -p 80:80 --network my_network wordpress`

4. Build an image from dockerfile and upload it to Dockerhub  
`docker build . -f ./TaskBoard.WebApp/Dockerfile -t dockerhub_username/dockerhub_repo`  
`docker build` - building the image
`.` - set the working dir
`-f ./TaskBoard.WebApp/Dockerfile` - path to the Dockerfile
`-t dockerhub_username/dockerhub_repo` - path to the Dockerhub repository

Docker Cheatsheet:
`docker build` - build image from dockerfile
`docker run` - run an existing dockerfile (if not local, it will search from the net)
`docker network create my_network` - create a network
`docker network inspect my_network` - view details about the network
`docker network -ls` - view all networks in the current docker engine
`-p 1234:1234` - define the port
`-e SOME_VARIABLE=variable_value` - setup an environment variable (can be set more than one)
`--network network_name` - setup the network. If no network provided, the container is connected to the default (bridge)
`-v volume_name:/path` - map a volume to a local path/dir
`--name container_name` - container name
`--rm --name container_name` - remove the container if exists and create it again
`-d` - detached mode
`-i` - interactive mode
`-t` - terminal mode
`-dit` - detached and interactive mode and enter docker's terminal 
`-p` - if nothing after it, it means password, so password will be required
`docker network connect network_name container_name` - add container to network

