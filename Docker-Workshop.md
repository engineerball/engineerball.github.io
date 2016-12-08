# LAMP with Docker
## 1. Introduction to Docker
1. What is Docker?
2. VMs VS Containers

  ![alt text](https://s3.amazonaws.com/media-p.slid.es/uploads/560276/images/2975971/pasted-from-clipboard.png "VM")

3. Where does Docker come in?

  1. Ease of use
  2. Speed
  3. Docker Hub (Repository)
  4. Modularity and Scalability

## 2. Fundamental Docker Concepts

![alt text](https://s3.amazonaws.com/media-p.slid.es/uploads/560276/images/2976104/docker-architechture.png "Docker concepts")

  1. Docker Host, Docker Engine

    Docker engine is the layer on which Docker runs.

  2. Docker Client

    The Docker Client is what you, as the end-user of Docker, communicate with.

  3. Docker Daemon

    The Docker daemon is what actually executes commands sent to the Docker Client — like building, running, and distributing your containers. The Docker Daemon runs on the host machine, but as a user, you never communicate directly with the Daemon.

  4. Dockerfile

    A Dockerfile is where you write the instructions to build a Docker image.

  5. Docker Image

    Images are read-only templates that you build from a set of instructions written in your Dockerfile.

  6. Docker Container    

    Wraps an application’s software into an invisible box with everything the application needs to run. That includes the operating system, application code, runtime, system tools, system libraries, and etc. Docker containers are built off Docker images.

    ![alt text](https://cdn-images-1.medium.com/max/800/1*hZgRPWerZVbaGT8jJiJZVQ.png)

  7. Volumes

    Volumes are the “data” part of a container, initialized when a container is created. Volumes allow you to persist and share a container’s data.

  8. Docker registry

    A service responsible for hosting and distributing images. The default registry is the Docker Hub

## 3. Fundamental Docker commands

1. ``` docker pull ```

  ```
  Usage:  docker pull [OPTIONS] NAME[:TAG|@DIGEST]
  Pull an image or a repository from a registry
  Options:
    -a, --all-tags                Download all tagged images in the repository
        --disable-content-trust   Skip image verification (default true)  
        --help                    Print usage
  ```

2. ``` docker run ```

  ```
  Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
  Run a command in a new container

  Options:
    -d, --detach          Run container in background and print container ID
    -e, --env value       Set environment variables (default [])
    -i, --interactive     Keep STDIN open even if not attached
    --restart string      Restart policy to apply when a container exits (default "no")
                          Possible values are : no, on-failure[:max-retry], always, unless-stopped
    -p, --publish value   Publish a container's port(s) to the host (default [])
    --rm                  Automatically remove the container when it exits
    -t, --tty             Allocate a pseudo-TTY
    -v, --volume value    Bind mount a volume (default []). The format is `[host-src:]container-dest[:<options>]`. The comma-delimited `options` are [rw|ro]
    -w, --workdir string  Working directory inside the container
  ```

3. ```docker ps```
  ```
  Usage: docker ps [OPTIONS]
  List containers

  Options:
    -a, --all             Show all containers (default shows just running)
    -q, --quiet           Only display numeric IDs
  ```

4. ``` docker exec ```
  ```
  Usage:  docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
  Run a command in a running container

  Options:
    -i, --interactive    Keep STDIN open even if not attached
    -t, --tty            Allocate a pseudo-TTY
  ```
5. ``` docker logs ```
  ```
  Usage:  docker logs [OPTIONS] CONTAINER
  Fetch the logs of a container

  Options:
    -f, --follow         Follow log output
  ```
6. ```docker commit```
  ```
  Usage:  docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
  Create a new image from a container's changes

  Options:
    -m, --message string   Commit message
  ```
7. ```docker images```
  ```
  Usage:  docker images [OPTIONS] [REPOSITORY[:TAG]
  List images
  Options:
    -a, --all             Show all images (default hides intermediate images)
  ```
7. ```docker start```
  ```
  Usage:  docker start [OPTIONS] CONTAINER [CONTAINER...]
  Start one or more stopped containers
  ```
8. ```docker stop```
  ```
  Usage:  docker stop [OPTIONS] CONTAINER [CONTAINER...]
  Stop one or more running containers
  ```
9. ```docker rm```
  ```
  Usage:  docker rm [OPTIONS] CONTAINER [CONTAINER...]
  Remove one or more containers
  Options:
    -f, --force     Force the removal of a running container (uses SIGKILL)
  ```
10. ```docker rmi```
  ```
  Usage:  docker rmi [OPTIONS] IMAGE [IMAGE...]
  Remove one or more images
  Options:
    -f, --force      Force removal of the image
  ```

## 4. Fundamental Dockerfile

0. FROM

  The FROM instruction sets the Base Image for subsequent instructions. As such, a valid Dockerfile must have FROM as its
  first instruction. The image can be any valid image – it is especially easy to start by pulling an image from the
  Public Repositories.

  ```
  FROM <image>:<tag>
  ```

1. MAINTAINER

  The MAINTAINER instruction allows you to set the Author field of the generated images.

  ```
  MAINTAINER <name>
  ```

2. RUN

  The RUN instruction will execute any commands in a new layer on top of the current image and commit the results. The
  resulting committed image will be used for the next step in the Dockerfile

  ```
  RUN <command>
  ```
3. CMD

  There can only be one CMD instruction in a Dockerfile. If you list more than one CMD then only the last CMD will take
  effect.

  ```
  CMD ["executable", "param1", "param2"] exec form, this is the preferred form)
  ```

4. LABEL

  The LABEL instruction adds metadata to an image. A LABEL is a key-value pair. To include spaces within a LABEL value,
  use quotes and backslashes as you would in command-line parsing.

  ```
  LABEL <key>=<value> <key>=<value> <key>=<value>
  ```
5. EXPOSE

  The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime. EXPOSE does
  not make the ports of the container accessible to the host.

  ```
  EXPOSE <port> [<port> ...]
  ```

6. ENV

  The ENV instruction sets the environment variable <key> to the value <value>. This value will be in the environment of
  all “descendant” Dockerfile commands and can be replaced inline in many as well.

  ```
  ENV <key> <value>
  ENV <key>=<value>
  ```

7. ADD

  The ADD instruction copies new files, directories or remote file URLs from <src> and adds them to the filesystem of the
  container at the path <dest>.

  ```
  ADD <src> <dest>
  ```

8. COPY

  The COPY instruction copies new files or directories from <src> and adds them to the filesystem of the container at the
  path <dest>.

  ```
  COPY <src> <dest>
  ```

9. ENTRYPOINT

  An ENTRYPOINT allows you to configure a container that will run as an executable.

  ```
  ENTRYPOINT ["executable", "param1", "param2"] (exec form, preferred)
  ```

  Both CMD and ENTRYPOINT instructions define what command gets executed when running a container. There are few rules
  that describe their co-operation.

    * Dockerfile should specify at least one of CMD or ENTRYPOINT commands.
    * ENTRYPOINT should be defined when using the container as an executable.
    * CMD should be used as a way of defining default arguments for an ENTRYPOINT command or for executing an ad-hoc
    command in a container.
    * CMD will be overridden when running the container with alternative arguments.

10. VOLUME

  The VOLUME instruction creates a mount point with the specified name and marks it as holding externally mounted volumes
  from native host or other containers.

  ```
  VOLUME ["/data"]
  ```

11. USER

  The USER instruction sets the user name or UID to use when running the image and for any RUN, CMD and ENTRYPOINT
  instructions that follow it in the Dockerfile.

  ```
  USER daemon
  ```

12. WORKDIR

  The WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow
  it in the Dockerfile.

  ```
  WORKDIR /path/to/workdir
  ```


#### Dockerfile example

  ```
  # Nginx
  #
  # VERSION               0.0.1

  FROM      ubuntu
  MAINTAINER Victor Vieux <victor@docker.com>

  LABEL Description="This image is used to start the foobar executable" Vendor="ACME Products" Version="1.0"
  RUN apt-get update && apt-get install -y inotify-tools nginx apache2 openssh-server
  ```
## 4. How to run Docker LAMP containers

0. Checkout php example code

  ```bash
  $ git clone https://github.com/engineerball/bike bike && cd $_
  ```

1. Mysql

  [docker MySQL image repository](https://hub.docker.com/_/mysql/)

  ```bash
  $ docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -v /var/lib/mysql:/varlib/mysql mysql:5.7
  ```

2. Apache + PHP-7.1

  [docker PHP-7.1 image repository](https://hub.docker.com/_/php/)

  ```bash
   $ docker run -d --name my-php-example --link mysql:mysql -v $PWD:/var/www/html -p 8080:80 php:7.1-rc-apache /bin/bash -c 'docker-php-ext-install mysqli pdo_mysql tokenizer; a2enmod rewrite; apache2-foreground'
  ```

3. phpMyAdmin

  [docker phpMyAdmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/)

    ```bash
    $ docker run --name phpmyadmin -d --link mysql:db -p 8081:80 phpmyadmin/phpmyadmin
    ```

4. Access via port 8080 and 8081

## 5. How to create Dockerfile (PHP-7.0 with example code (Laravel5-example))

  1. Clone code repositroy

    ```
    git clone https://github.com/itobuz/shila-laravel-backend my-php-example && cd $_
    ```

  2. Install dependency files by composer

  ```
  docker run -it --rm -v ${PWD}:/var/www/html -w /var/www/html engineerball/php71-builder sh -c "composer install"
  ```

  3. Add laravel .htaccess

  ```bash
  cat <<'EOF' > .htaccess                                                                               
   <IfModule mod_rewrite.c>
    RewriteEngine on

    RewriteRule ^(.*)$ public/$1 [L]
   </IfModule>
  EOF
  ```  

  4. Create Databasee

    use phpmyadmin

  4. Edit .env file

    Copy .env.example to .env

    ```
    cp .env.example .env
    ```

    And edit .env database setting
    ```
    DB_CONNECTION=mysql
    DB_HOST=mysql
    DB_PORT=3306
    DB_DATABASE=workshop
    DB_USERNAME=root
    DB_PASSWORD=my-secret-pw
    ```

    Run artisan command

    ```
    docker run -it --rm -v ${PWD}:/var/www/html -w /var/www/html engineerball/php71-builder sh -c "php artisan key:generate"
    docker run -it --rm -v ${PWD}:/var/www/html -w /var/www/html --link mysql:mysql engineerball/php71-builder sh -c "php artisan migrate"
    docker run -it --rm -v ${PWD}:/var/www/html -w /var/www/html --link mysql:mysql engineerball/php71-builder sh -c "php artisan db:seed"
    docker run -it --rm -v ${PWD}:/var/www/html -w /var/www/html --link mysql:mysql engineerball/php71-builder sh -c "php artisan storage:link"
    ```

  4. Add    

  ```Dockerfile
  FROM php:7.1-rc-apache
  MAINTAINER <your name>

  # Install php module
  RUN docker-php-ext-install tokenizer pdo_mysql

  # Copy source to /var/www/html
  COPY . /var/www/html

  RUN chmod -R 777 /var/www/html/storage

  # Enable mod rewrite
  RUN a2enmod rewrite
  ```


## 6. How to build Dockerfile

``` bash
$ docker build -t $USER/my-php-example .
```

### 7. How to run Docker image

```bash
$ docker run -it --link mysql:mysql -p 8082:80 --name php71-example $USER/my-php-example
```

## 7.How to push Docker images to Docker Registry

``` bash
$ docker login
$ docker commit
$ docker push $USER/my-php-example
```


***
# Jenkins Pipelines
## 1. Old ways
## 2. New ways
## 3. Requirements
## 4. Jenkins Job DSL Plug-In (Groovy Scripts)
1. Whats?
2. Example

## Pipelines as a Code

## Jenkins Jobs DSL Step
1. Node
2. Stage
3. Checkout
4. Execute
5. Publishes

## Pipelines examples
1. Working with files
2. Pass files between stage
3. Parallel Execution of Steps
4. Use existing plugins in pipeline
5. Manual steps - confirmation dialog

## Let's do it
