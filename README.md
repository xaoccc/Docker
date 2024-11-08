# Docker
Docker training

1. MyWebsite:  
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


