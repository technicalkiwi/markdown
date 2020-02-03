# Install Docker - Community Edition

Uninstall Old Versions
`$ sudo apt-get remove docker docker-engine docker.io containerd runc`

Install packages to allow apt to use a repository over HTTPS:
`sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common`

Add Docker’s official GPG key
`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`

Verify that you now have the key with the fingerprint
`sudo apt-key fingerprint 0EBFCD88`

<pre>
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
</pre>

Add in Docker Repository
`sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`

Update the apt package index
`sudo apt-get update`

Install docker and containerd
`sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose`

Verify The Docker Installation is working
`sudo docker run hello-world`

It Should output the below
<pre>
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete
Digest: sha256:9572f7cdcee8591948c2963463447a53466950b3fc15a247fcad1917ca215a2f
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

</pre>