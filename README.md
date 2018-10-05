# CIDER
Container Isolated Development EnviRonment(s)

CIDER is an attempt to eliminate the complexity of programming language versions, virtual environments, and package management using Docker containers.

The first of these experiments addresses python 3.7 on Alpine Linux.

## Installation

You must set a github personal access token to enable this container to function using git. Further, you must specify the repository that this container will hold. Finally, set a name for the image. I use the repo name minus the .git extension. YMMV.

Build the image:

    docker build --squash --build-arg GITHUB_TOKEN=<YOUR_TOKEN_HERE> --build-arg GITHUB_REPOSITORY=https://github.com/<YOUR>/<REPO>.git .

Copy the tag from the newly-built image:

    docker images |more

Paste the tag into this command and set the name of the image:

    docker tag <TAG_COPIED_FROM_PREVIOUS_COMMAND> <YOUR_REPO_NAME>:latest

Run the new image:

    docker run -it <YOUR_REPO_NAME>:latest
