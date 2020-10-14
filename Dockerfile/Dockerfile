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



