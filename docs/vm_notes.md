
# Getting Started
1. To set up a virtual machine, go to <https://vcm.duke.edu/reservations/new/vm>, and under "Application and Operating System”, select “Ubuntu16.04”.

2. ssh to vcm@HOSTNAME where `HOSTNAME` comes from
   <https://vcm.duke.edu/reservations/> click on "View password" for password.

3. Run `sudo apt-get install docker.io tmux` to install docker and tmux

<!-- 4. Run `sudo apt-get install emacs24-nox ` to install emacs -->


# Configure Docker to run as a non-root user
1. Create the docker group: `sudo groupadd docker`

2. Add your user to the docker group: `sudo usermod -aG docker $USER`

3. Log out and log back in so that your group membership is re-evaluated.

4. Verify that you can run docker commands without sudo: `docker run hello-world`

# Setup SSH Keys
0. Run `tmux new -s setup_vm` to start a tmux session named "setup_vm"

1. Follow the
   [Github instructions](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key)
   to Generate an SSH key on the VM.

2. Run `eval "$(ssh-agent -s)"` to start ssh-agent

3. Run  `ssh-add ~/.ssh/id_rsa` to add your key to the agent.  You will be asked to enter the passphrase
for the SSH key.

4. Run `clear; echo "-------"; cat ~/.ssh/id_rsa.pub; echo "-------"` to show the public part of the SSH key
you just generated, then copy it (select everything between the two sets of "-------")

6. Starting at step #2, follow the 
   [Github instructions](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)
   for adding a new SSH key.

# Setup Git and pull the project repo
The following will configure git with your name and email address
1. Run `git config --global user.name "MY_NAME"`, replacing
**MY_NAME** with your actual name

2. Run `git config --global user.email "MY_EMAIL"`, replacing
**MY_EMAIL** with your actual email address

3. Run `git clone git@github.com:granek/cimseq.git` to clone
   the repo from GitHub.  You will be asked to enter the passphrase
   for the SSH key you generated above.  You will be prompted to
   confirm the github.com RSA key fingerprint, if it is
   "16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48", then type `yes`.


# Docker
## Setup Rstudio Docker
1. Do `cd ~/cimseq/compute_environment/docker` to change into the
   directory with docker info.

2. Do `cp local_docker_setup.sh.EXAMPLE local_docker_setup.sh` to
   generate a working version of the docker configuration script.

3. Optional: edit `local_docker_setup.sh` to change RStudio password

## Build Docker Image and Run
1. Run `bash docker_build.sh` to build Docker image

2. Run `bash start_rstudio_docker.sh rstudio`

3. The above command should print out information about opening
RStudio

	1. Open the URL printed as *RStudio URL* in a web browser

	2. Use the *RStudio Username* and *RStudio Password* to log in to RStudio Server

## Setup RStudio Project
1. Run the New Project command (from the Project menu)

2. Choose to create a new project from an **Existing Directory**

3. Select `~/cimseq`

4. Click Create Project

You should now be ready to work!
