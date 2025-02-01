# Helpful Docker commands and code snippets

### CONTAINERS ###
`docker run --rm -it -p <port-number>:<port-number> -v $PWD:/<container-dir> -w /<container-dir> <image:tag> <command>
`docker stop $(docker ps -a -q) #stop ALL containers`
`docker rm -f $(docker ps -a -q) # remove ALL containers`
`docker rm -f $(sudo docker ps --before="container_id_here" -q) # can also filter`

### Exec into container
`docker exec -it $(docker container ls  | grep '<seach_term>' | awk '{print $1}') sh`

### Exec into container on windows with Git Bash
`winpty docker exec -it $(docker container ls  | grep '<seach_term>' | awk '{print $1}') sh`

### Helps with error: 'unexpected end of JSON input'
`docker rm -f $(docker ps -a -q) # Remove all in one command with --force`
`docker exec -i -t "container_name_here" /bin/bash # Go to container command line`

### Docker build
`docker build -t my-image-name .
Some [[Docker files]] for custom docker image
- Node & chromium for Front end development & testing
- Keycloak image