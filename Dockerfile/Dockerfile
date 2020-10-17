Dockerfile
==========
Docker can build images automatically by reading the instructions from a Dockerfile.
A Dockerfile is a text document that contains all the command instructions that 
user could call from commandline for assembling an image.

'Dockerfile' name is case-sensitive.

Usage
=====

$ docker build -f /path/to/Dockerfile -t repo_name/image_name:tag_name .

The docker build command builds an image from a Dockerfile.The Dockerfile location can be a PATH or URL.

-> The PATH is a directory on a local filesystem.
-> The URL is a Git repository location.

'As a good practice,we should have a seprate location for the Dockerfile and all the other relavent files 
and directories required for building the new image'

The build is run by the Docker daemon not by the CLI.The build sends the entire context to the daemon.

We can ignore the files and directories by adding the .dockerignore file in the build area.

Usually Dockerfile is located in the root of the build area but we can specify the other path by using the -f flag with docker build.

We can tag image into multiple repositories during the build :

$ docker build -f /path/of/Dockerfile -t repo_name/image_name:tag_name -t repo_name/image_name:tag_name .

Before docker daemon runs the instructions in the Dockerfile,it performs a validation check of the Dockerfile.

The Docker daemon runs the instructions from the Dockerfile one-by-one and committing the changes to a new image.

Each instructions in the Dockerfile is run independently.


Format
======
Dockerfile format:

#Comment
INSTRUCTION arguments

The instruction is not case-sensitive.However,it is good to keep it in UPPER case so that
instructions can be distinguish from the arguments.

A Dockerfile must begin with a 'FROM' instruction,which tell which image template need to be
used during the build process.

Before the 'FROM' instruction we can give 'Parser Directives' or 'Comments' or 'Globally scoped ARGs'.

.dockerignore file
==================
Before docker build sends the Dockerfile context to the daemon,it looks for a file named 
.dockerignore in the root directory of the context.

.dockerignore file contains the list of files and directories which need to be ignored during
the build process.

Example:
========
# comment  ## ignored
./temp*	   ## exclude files and directories whoes name start with temp
*/*/temp*  ## exclude files and directories,sub-directories which include temp
temp?      ## exclude files and directories /temp ,/tempa or /tempb are excluded
!README.md ## exception

FROM
====

FROM --platform=<platform> <image>:<tag> AS <name>
or
FROM --platform=<platform> <image>:<@digest> AS <name>

The FROM instruction initializes a new image build stage and sets the base image for subsequent instructions.

FROM can appeared multiple times in the Dockerfile

-> **ARG is the only instructions that may precede FROM in the Dockerfile.
   ARG can hold any argument that can be used in the instruction below FROM.
   
   ARG BUILD_VERSION=latest
   FROM ubuntu:${BUILD_VERSION}

-> **platform flag can be used to specify the platform of the base image template,like linux/amd64, linux/arm64 or window/amd64.

-> <image> can be any valid image template name from docker hub repository

-> **<tag> and <@digest> can be obtained from docker hub repository.If it is ommited build will consider <latest>

RUN
===

RUN has 2 forms:

-> RUN <command> (shell form,the default shell for the command is /bin/sh -c)
   The default shell can be override by using SHELL instruction.

-> RUN ["executable","param1","param2"] (exec form)

The RUN instruction execute the command on the top of the new image layer.

RUN /bin/bash -c 'source $HOME/.bashrc; \
echo $HOME'
or
RUN ["/bin/bash","-c","echo hello world"]

CMD
===

The CMD instruction has three forms:

-> CMD ["executable","param1","param2"] (exec form)
-> CMD ["param1","param2"] (as default parameter for ENTRYPOINT)
-> CMD command param1 param2 (shell form)

There can be only one CMD instruction in a Dockerfile.If we give multiple CMD instructions
then the last CMD instruction will be executed.

**RUN/CMD. RUN runs a command and commits the result.CMD does not execute anything 
at the build time.

LABEL
=====
The LABEL instruction add metadata to an image.A LABEL is a key-value pair.

LABEL <key>=<value> <key>=<value>

EXPOSE
======
The EXPOSE instruction informs Docker that the container listens on the specified
network ports at runtime.Ports can be TCP or UDP and the default is TCP if protocol is not
specified.

The EXPOSE instruction does not actually publish the port,it is just a documentation between
the person who build the image and the person who runs the container.

To actually publish the port at the run time of docker we need to give the '-p' flag on
docker run or the '-P' flag to publish all exposed ports and map them to high-order ports.

EXPOSE 80/udp
or
EXPOSE 80/tcp
EXPOSE 80/udp

EXPOSE settings can be override by using 'p' flag.

ENV
===
The ENV instruction sets the environment variable.It is formatted in <key> <value>

ENV MYVAR="Hello World"

The above environment variable will remain persist when a container runs from the resulting image.
The set environment variable can be checked with docker inspect command or it can be changed
during the docker run command 'docker run --env <key>=<value>'

ADD
===

ADD has two forms 

#shell
ADD --chown=<user>:<group> <src> <dest>

#exec
ADD --chown=<user>:<group> ["<src>","<dest>"]

The ADD instruction copies the local file into the image.
The advantage of using ADD is that,it also performs the action
on the file i.e

-> if i want to copy a tar.bz2 file from local to image,it will copy as well
   as extract the tar file.
-> if i give the url path in <src>,it will download the file from the given
   url in the image <dest> path.

COPY
====

COPY has two forms

#shell
COPY --chown=<user>:<group> <src> <dest>

#exec
COPY --chown=<user>:<group> ["<src>","<dest>"]

The COPY instruction copies the the local file into the image path,same
as ADD instruction.Only difference between COPY and ADD is that, COPY
does'nt performs the action just like ADD instruction does on the files which need to be copied in the image path.

We need to give the RUN instruction after performing the COPY instruction,
in case we need to perform some action on the copied file.

ENTRYPOINT
==========

The ENTRYPOINT instruction gets executed when running a container.A dockerfile
can have multiple ENTRYPOINT but only the last one will be executed.

ENTRYPOINT and CMD works together,CMD works as a default argument of the ENTRYPOINT.

FROM ubuntu
ENTRYPOINT ["top","-b"]
CMD ["-c"]

#exec
ENTRYPOINT ["<executable>","<param1>","<param2>"]

#shell
ENTRYPOINT command param1 param2


