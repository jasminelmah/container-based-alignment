


## Singularity on Farnam

Connect to Farnam (on windows use [mobaxterm](http://docs.ycrc.yale.edu/clusters-at-yale/access/#connect-from-windows)). After you're logged in, set your group to the class group so that files you create will be owned properly.

``` bash
ssh netid@farnam.hpc.yale.edu
newgrp eeb723
```

From the login node, allocate an interactive job with `srun`.

``` bash
# interactive session with 2 cores and default 10GiB of RAM
srun -A eeb723 --pty -p interactive -c 2 bash
```

Choose a working directory and band-mount it to your container

``` bash
# if you prefer a different directory use that instead
mkdir -p /gpfs/ysm/project/eeb723/${USER}/eeb723-seqaln
singularity shell --shell /bin/bash -B /gpfs/ysm/project/eeb723/${USER}/eeb723-seqaln:/data/eeb723-seqaln docker://eeb723/course_docker
```

This completes the assigned exercise.

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
