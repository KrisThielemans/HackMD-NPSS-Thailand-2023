# Technical Support for the SIRF workshop



## Do I need to install SIRF for the training?

We provide a cloud solution for trainees that does not require installation. We generally recommend that you will use our cloud set-up, also because some exercises will benefit highly from access to GPU.

You should receive an email with your account details in the near future. Once you have your account details, you can head to https://training.jupyter.stfc.ac.uk/.

Select `Training School for SIRF and CIL GPU` and wait a few minutes for your server to be launched. For running the Deep Learning notebooks, the servers without GPUs will give a Kernel Restarting error (so use a server with a GPU).

Note that the cloud solution will only be available from Wednesday and remain available for about 1 week after the school. 


### Jupyterhub and SIRF-Exercises
On the STFC Cloud jupyterhub, https://training.jupyter.stfc.ac.uk/ you will find all the software, the notebooks and the data pre-installed. However, you will still need to configure the `SIRF-Exercises`.

**Open a terminal** and type the following:

```
cd ~/SIRF-Exercises
git pull
./scripts/download_data.sh -w ./working_dir -p -m
```
(If you have already run some notebooks, please check the [update instructions](#SIRF-Exercises-update-instructions) instead of `git pull`.)
These commands will set the working directory to `working_dir` (in the current directory) so that the notebooks will run without (hopefully) problems in finding/opening/working with the data. All the output of your notebooks will be found in a subdir of `~/SIRF-Exercises/working_dir`.

## How do I update to the latest software on jupyterhub

Hopefully this should not be necessary, but if you are instructed to do so, open `File` and click on `Hub Control Panel` at the end of the menu below
![](https://i.imgur.com/e0iHJDy.png)

Then click on the BIG RED BUTTON
![](https://i.imgur.com/UTmGpzn.png)

In the next page click the on `Start my server` and you will be presented with a long list of choices. Choose the `Training School for SIRF and CIL GPU
For small jobs and prototyping: 10 CPUs, 60GB RAM and GPU. For Training School for SIRF and CIL` option below if you need a GPU or `Training School for SIRF and CIL no GPU` if you don't need one. Then clic    k start


![](https://i.imgur.com/GHCxHv2.png)









## matplotlib 
If you find the figures are a bit small and you can't really see anything in the images, then you can change the default size of the matplotlib figures at the beginning of the notebook right after importing matplotlib.pyplot. E.g.:
`import matplotlib.pyplot as plt`
`plt.rcParams["figure.figsize"] = (16,8)`


## Brainweb
If you run into the following error:
![](https://i.imgur.com/UEOnzvQ.png)

then the brainweb package has not been installed. In order to add this package open a terminal
![](https://i.imgur.com/awTPYRv.png)

and type`pip install brainweb` and hit enter:
![](https://i.imgur.com/plmrdT3.png)



## How do I install SIRF and CIL myself?
If you choose to install and run the training material locally **no support will be given during the workshop day**, but feel free to ask Kris Thielemans for pointers.


If you really want to do this, **please build the software yourself and use the Git master of SIRF, STIR and SIRF-Exercises.** 

Instructions below are for SIRF v3.4.0 (to be released in the next few days) and STIR v5.1. **We recommend to wait until the 3.4.0 VM and docker images are available.**

If you downloaded a previous version of the VM, you can try to [update it](https://github.com/SyneRBI/SIRF/wiki/Basic-usage-of-the-VM#updating-your-vm).
This will likely work, but we haven't tested this, so it is **NOT** recommended.

We provide binaries in 2 forms:
* an Oracle VirtualBox Virtual Machine. Information on installation and usage is on [this page](https://github.com/SyneRBI/SIRF/wiki/SyneRBI-Virtual-Machine).
* a Docker image on [dockerhub](https://hub.docker.com/r/synerbi/sirf/tags?page=1&ordering=last_updated), see instructions [here](https://github.com/SyneRBI/SIRF-SuperBuild/tree/master/docker#readme). (Use the `service` image, or if you are on Linux and have a GPU,  `service-gpu`)

Note: these binary distributions are 4GB or more.

* You can also build the software yourself from source if you're adventurous. SIRF and CIL can be installed together via the [SIRF-SuperBuild](https://github.com/SyneRBI/SIRF-SuperBuild/tree/master/#readme).
 [This wiki page](https://github.com/SyneRBI/SIRF/wiki/Installation-instructions) tells you how. Please set `BUILD_CIL=ON` in CMake.

### What minimum hardware requirements do you have for a local installation?

Some of the exercises will run on a standard laptop, but others will highly benefit from a multi-core processor, and many of the CIL exercises as well as the deep-learning exercises are only feasible on Linux with a GPU with CUDA 10 or later.

Total data-size download is about 24GB.

### I've got a Docker Image or the VM, what now?

Please check the [SIRF-Exercises/DocForParticipants](https://github.com/SyneRBI/SIRF-Exercises/blob/master/DocForParticipants.md). Once you have the Jupyter notebook running, the password is `virtual`. We recommend that you go to `SIRF-Exercises/notebooks/Introductory` and open the `introduction` notebook to start.

### VirtualBox VM, what is the password?
To log in into the VM the `sirfuser` user has `virtual` as password.
The password for the jupyter server on the VM is `virtual` again. (Also on docker.)

## SIRF-Exercises update instructions

To update the notebooks to the latest version (only do this if instructed to)

 1. Close any running notebooks (The 'stop' symbol on the sidebar accesses 'Running Terminals and Kernel's->'Shut Down All').
 2. Open a terminal via the Jupyter interface and change directory to where the exercises are:


- cloud: `cd ~/SIRF-Exercises`
- VM: `cd ~/devel/SIRF-Exercises`
- docker: `cd /devel/SIRF-Exercises`

and copy paste the following (potentially modify your email/name, but this actually doesn't matter as long as you don't `git push` anywhere else)
```
git config --global user.email you@example.com
git config --global user.name "Your Name"
cp -rp notebooks notebooks-modified
git checkout -b notebooks-modified
git add .
git commit -m "my modifications"
git checkout master
git pull
```
(Note that to paste in a Jupyter terminal, you will likely have to right-click, or similar on MacOS. It is recommended to use "paste as plain text" if that's an option that appears for you.)

After this, you should have a copy of your modified notebooks in `SIRF-Exercises/notebooks-modified`. You can also get back to them via the `git` command, but this is for advanced users only.

### location of SIRF-Exercises
- cloud: `~/SIRF-Exercises`
- VM: `~/devel/SIRF-Exercises`
- docker: `/devel/SIRF-Exercises`

## SIRF-Exercises backup instructions

It is of course recommended to make some backups of your own notebooks to your local computer system. You can download notebooks via the Jupyter interface.

Simply select a notebook, right click and click download.


## Some errors opening a notebook

### "File load error: Forbidden"

We are not sure when this happens, but closing the browser window and reconnecting to the STFC cloud seems to resolve this (it will connect to the same session so you should not loose any data).

## Some errors running the notebooks

### Run-time error "the reconstruction engine output may provide more information"
When running the SIRF notebooks, you might encounter an error message saying "*the reconstruction engine output may provide more information*" - so where is this "*reconstruction engine*" and where you can you get "*more information*". 

The short answer is: the text above that error message is hopefully helpful enough to find out what is wrong.

The long answer is a bit more complicated and depends on how you are running the notebooks. So here are some possible cases:
#### MR notebooks
The *reconstruction engine* then refers to Gadgetron
* You have started Gadgetron via a terminal via Jupyter: go to its  browser window.
* You are running a notebook from a VM instance. Then you might get more information in the VM terminal where you started jupyter notebooks from.
#### PET or SPECT notebooks
The *reconstruction engine* then refers to STIR. By default, STIR will output to warnings to terminal where you started the jupyter notebook, but this is only visible on the VM. It is recommended to use the `MessageRedirector` mechanism illustrated in some of the notebooks.

#### `sirf.Reg` notebooks or functionality
The *reconstruction engine* then refers to NiftyReg (or niftiio). This might output to warnings to terminal where you started the jupyter notebook, but this is only visible on the VM.



## FAQs

### Q: I need to reset my JupyterHub passwords

This can't be done by the user, ask the instructors.


### Q: Docker: the `pull` fails or times-out
Probably best to try again after a while, but you can avoid the large download by building the docker image yourself (although the download of all the packages is still substantial). Try
```
./sirf-compose-server build sirf
# get some coffee
./sirf-compose-server up -d sirf
```


### Q: How do I reset the results from a notebook?
You can clear all output in Jupyter by selecting from the menu "Cell" -> "All Output" -> "Clear".

Then you should restart the Python kernel, "Kernel" -> "restart".

If you have previously pressed the Save and Checkpoint option on the File menu, then you can revert to a previous checkpoint.

You can also delete the working folder associated with the notebook by navigating to the `working_folder` (on the cloud, this is `SIRF-Exercises/working-dir`, on other systems, `SIRF-Exercises/data/working_folder`, finding the notebook directory, selecting the checkbox next to it, and clicking the red bin icon.)

We can't support fully "resetting" your notebook if you changed the code. (If you are a familiar git user you could `git restore` the file, but this is advanced)

 
### Q: How do I start the Gadgetron server?

If you are using Docker to serve Jupyter notebooks, you do not need to start Gadgetron (it is already running in the Docker container). In other cases, you need to open a terminal window and type `gadgetron`, see [our documentation](https://github.com/SyneRBI/SIRF-Exercises/blob/master/DocForParticipants.md#start-a-gadgetron-server). If you get an error message about port 9002 in use, then this probably means that you have a gadgetron server already running which is using port 9002.
 
### Q: How do I decrease the STIR output in PET/SPECT notebooks?

You can reduce that info/warning statements by redirecting the output to file. If not done yet, add the following at the top of the python scripts/notebook:


```python=
from sirf.STIR import MessageRedirector

msg_red = MessageRedirector('info.txt', 'warn.txt', 'errr.txt')
```
### Q: How can I access the jupyter notebooks?

The material of the course is in the form of [jupyter notebooks](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html):

The Jupyter notebook combines two components:

- **A web application**: a browser-based tool for interactive authoring of documents which combine explanatory text, mathematics, computations and their rich media output.
- **Notebook documents**: a representation of all content visible in the web application, including inputs and outputs of the computations, explanatory text, mathematics, images, and rich media representations of objects.


To run the course material **only the users of the VM** need to manually start the [`jupyter`](https://jupyter.readthedocs.io/en/latest/running.html) server. This is done by typing in a terminal on the VM:
```
jupyter lab --no-browser
```

In the docker instance and in the STFC cloud, the jupyter server is already running.

**To connect to the jupyter server** you need to use a browser from the **host** machine, i.e. your laptop and point to the following websites, depending on the solution you are running:

- https://training.jupyter.stfc.ac.uk for the STFC cloud (suggested)
- http://localhost:8888 or http://127.0.0.1:8888 for the VirtualBox VM
- http://localhost:9999 or http://127.0.0.1:9999 for the docker image

Strictly speaking SIRF and CIL do not require to connect to internet to work but the school material is only accessible via the jupyter server.


### Q: I want to use SIRF and CIL from MATLAB rather than Python. How can I do that?

This will be possible only for SIRF as **CIL is mainly written in Python** and does not exist as MATLAB toolbox. 

To achieve this, **you will need to build SIRF from source to interface to MATLAB**, you will need to go to https://github.com/SyneRBI/SIRF-SuperBuild and follow instructions of compiling there. This can be a challenge, and it's out of scope for this training school. Unfortunately, due to resource restrictions, we are no longer updating nor testing SIRF MATLAB support though.


## Your questions

If you have a question related to the above, please enter it below (click on "Edit"). Please do not modify the text above.



# Back to main
[Main page](https://hackmd.io/_BDuHkbrSVmyZBDze9MUEg?view)
