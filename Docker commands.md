# Helpful Docker commands and code snippets

### CONTAINERS ###
`docker stop $(docker ps -a -q) #stop ALL containers`
`docker rm -f $(docker ps -a -q) # remove ALL containers`
`docker rm -f $(sudo docker ps --before="container_id_here" -q) # can also filter`

# exec into container
`docker exec -it $(docker container ls  | grep '<seach_term>' | awk '{print $1}') sh`

# exec into container on windows with Git Bash
`winpty docker exec -it $(docker container ls  | grep '<seach_term>' | awk '{print $1}') sh`

# helps with error: 'unexpected end of JSON input'
`docker rm -f $(docker ps -a -q) # Remove all in one command with --force`
`docker exec -i -t "container_name_here" /bin/bash # Go to container command line`