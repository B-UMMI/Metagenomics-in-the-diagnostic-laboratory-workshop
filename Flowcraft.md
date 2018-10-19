---
Author: "C I Mendes" \
Date: "October, 2018" 
---

## FlowCraft


#### Overview

FlowCraft is a python engine that automatically builds nextflow pipelines by assembling pre-made ready-to-use 
components. These components are modular pieces of software or scripts that are written for nextflow and have
 a set of attributes, such as input and output types, parameters, directives, etc. 
 
 This modular nature allows them to be freely connected as long as they respect some basic rules, such as the 
 input type of a component must match with the output type of the preceding component. This way, nextflow 
 processes can be written only once, and FlowCraft is the magic glue that connects them, handling the linking 
 and forking of channels automatically. 
 
 Moreover, each component is associated with a docker image, which means that there is no need to install any 
 dependencies at all and all software runs on a transparent and reliable box.
 
FlowCraft can be useful for bioinformaticians with varied levels of expertise that need to executed genomic pipelines 
often and potentially in different platforms. Building and executing pipelines requires no programming knowledge.

- In depth documentation on flowcraft: https://flowcraft.readthedocs.io/en/latest/

- Project repository: https://github.com/assemblerflow/flowcraft

#### Installation

FlowCraft can be installed as a bioconda package, requiring Conda or Miniconda to be installed in your system.

`$ conda install flowcraft`

```
Instructions on how to install Conda  or MiniConda are available at https://conda.io/docs/user-guide/install/index.html

```
Alternatively, you can install via pip that should be available in your system if you already have a Python installation.

`$ pip install flowcraft`


In the system you're using we provide the in-development version of FlowCraft so you can access the metagenomic methods
that haven't been yet in an official distribution.

We need to make sure we have the required software for the installations (wget) and an appropriate directory to keep
those installations. In this case we'll be using the *Tools* directory in the system's home directory.
```
apt-get install wget 

mkdir Tools

cd Tools
```
First we installed Singularity with the following commands on the terminal:
```

VERSION=2.5.2
wget https://github.com/singularityware/singularity/releases/download/$VERSION/singularity-$VERSION.tar.gz
tar xvf singularity-$VERSION.tar.gz
cd singularity-$VERSION
./configure --prefix=/usr/local
make
sudo make install

cd ..

```

You can test your installation by running the `$ singularity ` command.


Secondly, we installed Nextflow and java-jre, for which nextflow dependes for its functioning.

``` 
apt-get install java-jre

wget -qO- https://get.nextflow.io | bash

```

We need to make the nextflow executable accessible to your system, so we need to add it's path to the *.bashrc* file.
The *pwd* command will output the full path of the nextflow executable location. Copy that output. 

`$ pwd` 

Now add the export for this Path to the bashrc file by running the following command:

`$ export PATH=<result_from_pwd>:$PATH >> ~/.bashrc`
`$ source ~/.bashrc`

Lastly, you just need to install Flowcraft (developer installation).
Flowcraft is hosted in GitHub, so a tool called *git* is necessary to download Flowcraft's source code.
This assumes that python3 is already installed in your system. FlowCraft is built in Python3 and it's required for 
it's functioning.

```
apt-install git

git clone https://github.com/assemblerflow/flowcraft.git
cd flowcraft

python3 setup.py install 

git checkout workshop

cd flowcraft

pwd

export PATH=<result_from_pwd>:$PATH >> ~/.bashrc
source ~/.bashrc
```

Now you can return to you home directory and invoke Flowcraft by calling the *flowcraft.py* program.

`$ cd ~`
`$ flowcraft.py -h`

``` 
Note: If you install the developmen version of flowcraft, you invoke it by calling *flowcraft.py* on the terminal.
If you installed from one of the distributions, only the latest release is avaiable, invokable by *flowcraft* on
the terminal. 
```


#### Building a Pipeline

###### The build mode

Pipelines are generated using the build mode of FlowCraft and the -t parameter to specify the components inside quotes.
The components are modular pieces of software or scripts. You can see the full list of components available with
the command `$ flowcraft.py build -l` or `$ flowcraft.py build -L` form a more comprehensive listing. 

In this session we'll use a pipeline with the following components: remove_host, fastq_trimmomatic,
metamlst, metaphlan_fq, megahit, pilon maxbin, metaphlan_fa, abricate and mlst. 

To build the pipeline, we use can use the following command:

`$ mkdir workshop_pipeline`

`$cd workshop_pipeline`

`$ flowcraft.py build -t "remove_host fastqc_trimmomatic (metamlst | metaphlan_fq | megahit pilon maxbin2 ( metaphlan_fq | abricate | mlst))" -o workshop.nf`

`$ ls`

We've just created a nextflow pipeline, saved in the workflow.nf file, but there's a lot of other files present in 
the directory.

You probably noticed that the pipeline created has more components than the ones who were defined in the command.

This is due to certain components having others as dependency. For example, the megahit compoment requires the 
integrity_coverage one. Yu can have an overlook of the pipeline created by opening the *workshop.html* file.

<DAG>

First we need to alter a the parameters of this pipeline. First, we change the database to be used in abricate by 
opeining the *params.config* file with `nano` and editing the line correspondent to the the *abricate_6_11* process.
We can see in that file that the input fastq file should be located in a folder named *fastq*, and have the *fq.gz 
termination. We can edit this in this file if we have the file with other terminations and/or other locations.

For now, we'll create a directory for the fastq files and we'll copy the files into this location. Copy only the files
corresponding to your sample number. You should copy two files, one for the DNA sequencing and other for the cDNA.

``` 
mkdir fastq

cp ~/Data/S[<sample_number>]*_{1,2}* fastq/
```


###### The recipes

Recepies are already implemented pipelines that can be built with a simple command identifying the pipeline you
want to build.

A recipe for the pipeline we just created above is already available in flowcraft, and instead of the steps above,
we can simply do:

`$ flowcraft.py build -r metagenomics_workshop -o workshop.nf`

If we open the params.config file, we can see that the database for the abricate is already the appropriate one.

we still need to create the folder for the fastq files and copy them right sample files to that location. 

``` 
mkdir fastq

cp ~/Data/S[<sample_number>]*_{1,2}* fastq/
```


#### Running a Pipeline

Now that are the files are in the right location, and the parameters have been checked and adjusted as necessary, 
you're ready to start your nextflow pipeline by executing the following command:

`$ nextflow run workshop.nf`

Nextflow keeps track of all the processes executed in your pipeline. If any unexpected error occurs of if you
need to modify any of the scripts parameters, you can cancel the pipeline execution with *Ctr + C* and then
restart it from the latest checkpoint with the command:

`$ nextflow run workshop.nf -resume`

###### The inspector mode

FlowCraft  offers an inspect mode for tracking the progress of a nextflow pipeline either directly in a terminal 
(overview) or by broadcasting information to the [flowcraft web application](https://github.com/assemblerflow/flowcraft-webapp) 
(broadcast).

Simply run flowcraft inspect -m <mode> in a new terminal in the directory where the pipeline is running.
In either run mode, FlowCraft will keep running (until you cancel it) and continuously update the progress of a 
pipeline. 

If the pipeline is interrupted or fails for some reason, FlowCraft should be able to correctly reset the 
inspection automatically when resuming its execution.

We'll be using the inspector mode in broadcast mode:

`cd ~/workshop_pipeline`

`$ flowcraft.py inspect -m broadcast`


#### Obtaining a Report

When the execution of your pipeline has terminated, you can obtain an interactive report broadcasted to the
[flowcraft web application](https://github.com/assemblerflow/flowcraft-webapp). 

`$ flowcraft.py report`

The results for each component in the pipeline can be found in the *results* directory, divided by category. 

