# Clone a Private GitHub Repository Into a Docker Container

See [article](https://nigeldavis.com/Notes/GitHub/ssh_keys) on creating and activating GitHub SSH keys. we are goinn to use SSH keys to authorize docker to clone the private repository.

Now that you have created an SSH key and acivated it on your github account we are ready to clone it into a docker container.

### Example Dockerfile

First we need to create a Dockerfile

```docker
FROM python:3.9

COPY github_key .
RUN eval "$(ssh-agent -s)" && \
    ssh-add github_key && \
    ssh-keyscan -H github.com >> /etc/ssh/ssh_known_hosts && \
    git clone git@github.com:username/repo.git
```

### Line by Line

```docker
FROM python:3.9
```

For this example I built my docker container from Python 3.9 but it doesn't matter what image you want to use

```docker
COPY github_key .
```

This copies the file **github_key** from the same directory that docker container is being built from into the container. In order for this to work you will have to create a copy of the key that you created in the previous article and add it to your project (make sure to add this file to .gitignore file if you plan on uploading the project).

```docker
RUN eval "$(ssh-agent -s)" && \
```

Start the ssh-agent in the background inside the docker container

```docker
    ssh-add github_key && \
```

Add your SSH private key to the ssh-agent

```docker
    ssh-keyscan -H github.com >> /etc/ssh/ssh_known_hosts && \
```

Import the public keys from github.com

```docker
    git clone git@github.com:username/repo.git
```

Clone the private repository. 

If you haven't used SSH keys before this format of this remote url is slightly different then cloning with the usual https url. To get this url you can go to your github repository page online and click the green **Code** button and select SSH and copy the remote url that appears.

Now your repository should be cloned into the docker container. You can now work with it however you like.

## Use Cases

- install a private python package using 
- cloning a project into a specific docker environment to test
