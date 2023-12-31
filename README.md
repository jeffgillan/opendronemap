# opendronemap

Open drone map is a command line tool that will create point clouds, orthomosaics, and DEMs from drone imagery using the SfM workflow

https://docs.opendronemap.org/

The easiest way to run ODM is to run it from an existing docker image which is found on dockerhub
`opendronemap/odm:3.3.0`

### 1. Clone this repository to your local machine
!!Warning: Cloning this repo will downdload 363MB of drone imagery to your local machine!!

`git clone https://github.com/jeffgillan/opendronemap.git`

### 2. Change directories into the newly cloned repository

`cd opendronemap`

### 3. Run the Container

```
docker run -ti --rm -v $(pwd):/datasets/code  opendronemap/odm:3.3.0 --project-path /datasets --skip-orthophoto --skip-report --pc-copc --pc-quality medium
```

This is what the command is doing:

* Run docker
* Not sure what flags `-it` do exactly
* `--rm` removes image after is has been run
* `-v` mounts a volume. In this case it is the present working directory (pwd) on my local machine. Within this directory there must be a sub-directory called `/images`. This is where ODM will look for all of the raw drone images. For our example, we have 41 jpeg drone images. 
* The directory is mounted to the directory `/datasets/code` inside the image
* `opendronemap/odm` is the name of the Docker image which is located on Dockerhub
* The rest of the arguments are flags and options. These are parameters to change how the processing is done. By default, ODM will run through the entire processing pipeline unless you say otherwise. Check out options at https://docs.opendronemap.org/arguments/

To run ODM with very quickly with low quality:
```
docker run -ti -v $(pwd):/datasets/code  opendronemap/odm --project-path /datasets --skip-orthophoto --skip-report --pc-las --skip-3dmodel --pc-quality lowest
```
### Outputs

Completing the processing will take some time and will depend on your local computing resources. Once finished, there will be many new files and directories within your repository. 

The new directories may not have the permissions you want. You can change the owner of the directories by typing `sudo chown -R username:username *`

Within the directory `odm_georeferencing` you will find .las, .laz, and .copc.laz point cloud imagery products. 



You can view the cloud optimized point cloud (.copc.laz) at https://viewer.copc.io/

