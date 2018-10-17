---
Author: "C I Mendes" \
Date: "October, 2018" 
---

## Nextflow and Software Containers


#### Reproducibility of a Program

One of the biggest challenges of running a software pipeline is the lack of reproducibility associated with the
many variations that can change from system to system. There's the version of the tool itself, the version of 
it's dependencies, and the commands you use. 

In metagenomics this problem is exacerbated by the lack of golden standards, but a major part passes through the
standardization and assessment of software. 

In Linux systems, there is a  myriad of open source tools available. Favouring the ones with clear documentation 
describing the methodology implemented, stating the version used and which parameters will enable the comparison of
results across tools. 

#### Software containers

Recently, software containers have been emerging as a solution to these problem. They are a way to address primary 
dependency issues and enable distributing and deploying scientific software in a runnable state.

A container image is a lightweight, stand-alone, executable package of a piece of software that includes everything 
needed to run it: code, runtime, system tools, system libraries and system settings.​ Containerized software will always 
run the same, regardless of the environment. Containers isolate software from its surroundings, for example differences
 between development and staging environments and help reduce conflicts between teams running different software on the
 same infrastructure.​

[Docker](https://www.docker.com/) and [Singularity](https://singularity.lbl.gov/) are the most widely used solutions, with Docker proving a 
repository, called [Docker Hub](https://hub.docker.com/) where people can deposit their images to be shared with the community. 

These tools remove the need of complicated and cumbersome software installations when trying to reproduce a 
methodology, as well as ensure that the tools you use for your won analysis can be shared as-is.  

Instructions for installing docker and singularity on Linux systems can be found [here](https://docs.docker.com/install/linux/docker-ce/ubuntu/#set-up-the-repository)
and [here](https://singularity.lbl.gov/install-linux). 



#### The Nextflow

[Nextflow](https://www.nextflow.io/) is a workflow manager that, being based on the dataflow programming model used 
for building parallelized, scalable and reproducible workflows using software containers, brings reproducibility to
 the next level.
 
 It provides an abstraction layer between the execution and the logic of the pipeline, which means that the same 
 pipeline code can be executed on multiple platforms, from a local laptop to high performance computing clusters.
 
 This makes this framework ideal for genomic pipelines as they are increasingly executed on large computer clusters
 to handle large volumes of data and/or tasks, keeping portability and reproducibility as central pillars.
 
 Nextflow is:
 
 - *Reactive workflow framework* - It creates pipelines with asynchronous (and implicitly parallelized) data streams.
 
 - *Programming DSL* - Has its own (simple) language for building a pipeline
 
 - *Containerized* - Integrations with container engines (such as Docker and Singularity) is supported out of the box.
 
 The creation of Nextflow pipelines was design for bioinformaticians familiar with programing, but its execution is
 for everyone. 
 
 ```
 Note: Instruction for installing Nextflow can be found [here](https://www.nextflow.io/docs/latest/getstarted.html). 
 ```
  
 There are many advantages to nextflow. There's no need to manage temporary input/output directories/files and no 
 need for custom handling of concurrency (parallelization). A single pipeline can support many scripting languages,
 such as Bash, Python, Perl, etc. Every process can run in a container, or all processes can share the same container.
 Nextflow implements checkpoints, supporting a resume functionality. Lastly, a nextflow pipeline can be hosted on 
 [GitHub](https://github.com/) and be run remotely, without requiring local installation.
 
 In the next chapter we'll see how we can take the most advantage of Nextflow with Flowcraft. 