# Alignment exercise

## Introduction

In this exercise you will align some Illumina sequencing reads to a reference
sequence. The goals of this exercise are to:

- Familiarize you with git tasks including forks, commits, and pull requests.
- Learn how to use an interactive session on the computing cluster
- Learn to use singularity on the computing cluster
- Walk you through read alignment, one of the most common tasks in genomic work

## The exercise  

### Start an interactive session on Farnam

Open a terminal on your laptop.
- On macOS or linux, open the program called Terminal
- On Microsoft Windows,  use
  [mobaxterm](http://docs.ycrc.yale.edu/clusters-at-yale/access/#connect-from-windows))
	instead of Terminal.

In the terminal, login with the following command wehre `netid` is your own
Yale netid. Note that you need to be on the Yale network, so if you are off campus
first VPN in. If you are not on the Yale network, you will get an error like
`ssh: Could not resolve hostname farnam.hpc.yale.edu`.

``` bash
ssh netid@farnam.hpc.yale.edu
```

If login is successful, you will see a bunch of text and then be left with a
prompt that looks something like this: `[netid@farnam2 ~]$`. You are now
connected to a login node.

After you're logged in, set your group to the class group so that files you
create will be owned properly.

``` bash
newgrp eeb723
```

There is no output from this command, if it works
you will just get another prompt.

Now allocate an interactive job with `srun`. This puts you on an interactive
compute node, which has enough resources for the exercise.

``` bash
# interactive session with 2 cores and default 10GiB of RAM
srun -A eeb723 --pty -p interactive -c 2 bash
```

If it is successful, your prompt will change to something like
`[netid@c13n03 ~]$`.

### Launch a singularity container

You will run the analyses in a singularity container that uses a docker
container with all the needed software for the analyses.

Choose a working directory (a folder for your analyses). Then launch a
singularity container and band-mount this directory to the container. Mounting
this folder that is Farnam to the container allows you to get files in and out
of the container.

``` bash
mkdir -p /gpfs/ysm/project/eeb723/${USER}/eeb723-seqaln
singularity shell --shell /bin/bash -B /gpfs/ysm/project/eeb723/${USER}/eeb723-seqaln:/data/eeb723-seqaln docker://eeb723/course_docker
```

If this works you will see output something like the following, which returns the prompt to you:

``` bash
Docker image path: index.docker.io/eeb723/course_docker:latest
Cache folder set to /gpfs/ysm/home/cwd7/.singularity/docker
[14/14] |===================================| 100.0%
Creating container runtime...
Exploding layer: sha256:54f7e8ac135a5f502a6ee9537ef3d64b1cd2fa570dc0a40b4d3b6f7ac81e7486.tar.gz
Exploding layer: sha256:ba93dfd291824441baa6a31fc8c4af5bb4f83c921d8ff3945b862407a14a3b3b.tar.gz
Exploding layer: sha256:c03738a8c9402d89e35cfc72c1ec9c1b86a0144ef256e27cf8a456a576c29c51.tar.gz
Exploding layer: sha256:ad62af4c2658eadf72867000904bd4b67ef763ca9d8ea3a33453642dfa3dcec8.tar.gz
Exploding layer: sha256:119baedb21a9b4ed9ede5d992f65007514bdc7d6bbf526d5a5c69281ee350618.tar.gz
Exploding layer: sha256:ea916453187e5d163e84363c0bca38c45514044b8461615778698de7e804fff4.tar.gz
Exploding layer: sha256:c1179c6680f5ee147fa3148b4b47277c4091e5407fd6dd7ae767e0ae98a3ba90.tar.gz
Exploding layer: sha256:8a0c826d2f5d303eb6b3caa9b46e79bdb3d6eafa90cf32aed4035f09f958d3a9.tar.gz
Exploding layer: sha256:882c188f4454c677b2e5efcd159c33b8fe8941355fdde0c6e0171aedc961bce2.tar.gz
Exploding layer: sha256:c797c633effb523ebfce4b651d3e8cbdc155fdfee8bdc7f1658d9be0a63dca97.tar.gz
Exploding layer: sha256:d753068e6af0d8d67eac8077397ec397544e5b3533c4ead1c046db471b402bea.tar.gz
Exploding layer: sha256:72376858bc9a87482269bc49fdecf7b65f3eedd76e5f45868b4c1df0dbe54a40.tar.gz
Exploding layer: sha256:37c53758a333554d0baeb574acfc4ea24eb870373db60eeb931fe75b8c10f93e.tar.gz
Exploding layer: sha256:53607fb60a0f35c9434818dc4d332c2eb9110e8a99e54c2f994177c3a92b1b54.tar.gz
Exploding layer: sha256:c6abb519bd9e4ac6c817d671248885a6463115f62c47db48398d9b05cd2437f9.tar.gz
Singularity: Invoking an interactive shell within container...

cwd7@c13n03:~$
```

You get the prompt to the interactive node back, but all the tools from the container are
now available to you.

### Run the analyses

Copy and paste the commands one by one from [alignment.sh](https://github.com/Yale-EEB723/container-based-alignment/blob/master/alignment.sh)
and run them at the prompt you got above. You don't need to run the lines that are blank or
that start with `#` (these are comments to explain the contents of the file to
humans).

### Submitting your results via GitHub.

Go to https://github.com/Yale-EEB723/container-based-alignment and click the
"Fork" button at the upper right. This creates your own fork of the assignment
repository.

Point your browser to your form of the repository. It will be something like
https://github.com/YourGitHubUsername/container-based-alignment . Click on the
green "Clone or download" button and copy the link there.

Open a Terminal window on your laptop. `cd` to a directory where you keep your
git repositories. Then clone your form of the repository (substitute your
GitHub username into the command below):

``` bash
https://github.com/YourGitHubUsername/container-based-alignment.git
cd container-based-alignment
open . # On macOS, this command opens the current folder in the Finder
```

This creates a local cone of your fork of the assignment repository. Open the
`questions.md` file within this folder within a text editor (I suggest Atom).
Answer the prompts, and save the file.

Commit and push the results back to GitHub:

``` bash
git commit -am "answered questions"
git push
```

Once the results are pushed to GitHub, return to the repo page at
https://github.com/YourGitHubUsername/container-based-alignment (substituting
in your GitHub Username).

Click the "New pull request" button. Then click the "Create pull request" button
and submit the pull request. This will notify the instructor that you have
submitted the assignment.

*This completes the assigned exercise.*

## Additional information

This section contains additional information that is not part of the assignment,
but that may be useful for context and your own future analyses.

### Running the exercise as a script

Above you coped and pasted the commands into an interactive shell one by one.
This is good to understand the exercise and is the way you may do some preliminary
analyses, but usually you will run analyses as scripts. This requires less
user intervention, is reproducible, and is less prone to human error.

The analyses presented here can be run as a script. First, make sure an output
folder called `/data/eeb723-seqaln` exists. Then from an interactive shell,
instead of copying and pasting the commands `cd` to this directory and
run the command `bash alignment.sh`.

### Running the analyses on other computers with Docker

These analyses can be run on computers other than the cluster from within a
docker container. Here are some instructions for how to do this on a couple
different operating systems.

#### Windows

Open a new command prompt by typing <kbd><img src=http://i.stack.imgur.com/B8Zit.png></kbd>+<kbd>R</kbd>, then enter `cmd` into the prompt and click OK

We need a folder to keep files generated from our analyses on your computer. Enter the following into your command prompt:

``` cmd
md %USERPROFILE%\Desktop\eeb723-seqaln
```

Next, start up the class environment in Docker:

```
docker run --rm -ti -v %USERPROFILE%\Desktop\eeb723-seqaln:/data/eeb723-seqaln eeb723/course_docker bash
```


#### macOS/linux

Open a new Terminal window (on a mac start up Terminal.app), then enter the following to set up a directory to keep files generated from our analyses on your computer.

``` bash
mkdir -p ~/Desktop/eeb723-seqaln
docker run --rm -ti -v ~/Desktop/eeb723-seqaln:/data/eeb723-seqaln eeb723/course_docker bash
```
