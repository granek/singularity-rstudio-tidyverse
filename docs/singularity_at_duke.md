# Getting a VM at Duke
1. Request a new VM from Duke's [Virtual Computing Manager](https://oit.duke.edu/help/articles/vcm-how-use-virtual-computing-manager) or [Research Toolkits](https://oit.duke.edu/what-we-do/applications/research-toolkits) (limited to faculty). Your VM should be based on "Ubuntu 16.04"

2. SSH to your new VM, and do all the following *on the VM*

# Use Tmux (Recommended)
3. Run `sudo apt-get install tmux` to install tmux
4. Once is is installed use `tmux new -s setup_server` to start a tmux session.  You should see a green band at the bottom indicating that you are in a tmux session.  Google "tmux tutorial" for help in using tmux. Its worth it!

# Install Singularity
This is a quick summary.  For details see [The Official Singularity Docs](https://www.sylabs.io/guides/2.5/user-guide/installation.html)
1. Run the following to install singularity pre-requirements
```
sudo apt-get update && \
    sudo apt-get install \
    python \
    dh-autoreconf \
    build-essential \
    libarchive-dev \
    squashfs-tools
```

2. Run the following commands to install singularity version 2.6.1.
```
VER=2.6.1

wget https://github.com/sylabs/singularity/releases/download/$VER/singularity-$VER.tar.gz

tar xvf singularity-$VER.tar.gz

cd singularity-$VER

./configure --prefix=/usr/local --sysconfdir=/etc

make

sudo make install
```

# Run an Image
https://singularity-hub.org/collections/2084/usage

# Set Up a User Account (Recommended)
5. To set up a new user account, run `sudo adduser NAME_OF_USER`, where you replace *NAME_OF_USER* with the username you would like to create

# Setup SSH Keys (Recommended)
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


7. Run the following to get the script that will download course material and the jupyter image
```
curl -O https://gitlab.oit.duke.edu/HTS2018/HTS2018-notebooks/raw/master/reproducibility/prep_local_jupyter.sh
```

8. Run `bash prep_local_jupyter.sh hts2018`  to download course material and the jupyter image, and run it. Follow the printed instructions for accessing the Jupyter instance running on your VM.

9. You will probably get one of the following warnings, depending on your browser, it is safe to ignore this
	- *Chrome*: "Your connection is not private"
	  1. Click *ADVANCED*
	  2. Click *Proceed to XXXXXXX (unsafe)*, where XXXXXXX is the URL of your VM
	- *Safari*: "This Connection Is Not Private"
	  1. Click *Show Details*
	  2. Click *visit this website*
	  3. Click *Visit Website*
	- *Firefox*: "Your connection is not secure"
	  1. Click *ADVANCED*
	  2. Click *Add Exception*
	  3. Uncheck the box next to *Permanently store this exception*
	  4. Click *Confirm Security Exception*






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



