---
description: Getting started with Groq.
---
# Groq Getting Started Guide

## Groq Links
- [Groq API](https://github.com/Groq/GroqAPI)
- [GroqFlow](https://github.com/groq/groqflow)

## Login and Groq Cards Available
Start by logging into ExCL's login node.
```bash
ssh login.excl.ornl.gov
```
This will create your home directory if you have not logged into ExCL before. From the login node, you can then login to a node with a Groq card.
```bash
ssh pcie
```

Here is a table of the Groq cards available:
| Hostname | Groq Cards |
|----------|------------|
| pcie     | 1          |

## Groq card and Slurm

The recommended way to access the Groq card is to reserve it through the Slurm resource manager.
Groq cards are available on machines in the groq partition. To reserve a node with a groq card for interactive use use the command.
```
srun -J groq_interactive -p groq --exclusive --gres="groq:card:1" --pty bash
```
> Where:\
> &#x20; `-J`, `--job-name=<jobname>` specifies the job name.  
> &#x20; `-p`, `--partition=<partition names>` specifies the partition name.  
> &#x20; `--exclusive` specifies you want exclusive access to the node.  
> &#x20; `--gres="groq:card:1"` specifies that you want to use 1 groq card.  

Non-interactive batch jobs can similarly be launched. 
```
sbatch -J groq_batch -p groq --exclusive --gres="groq:card:1" run.sh
```
> Where:\
> &#x20; `-J`, `--job-name=<jobname>` specifies the job name.  
> &#x20; `-p`, `--partition=<partition names>` specifies the partition name.  
> &#x20; `--exclusive` specifies you want exclusive access to the node.  
> &#x20; `--gres="groq:card:1"` specifies that you want to use 1 groq card.  

or specified in the script:
```bash
#SBATCH --job-name=groq_batch
#SBATCH --partition=groq
#SBATCH --exclusive
#SBATCH --gres="groq:card:1"
...
```

## Using the Groq Card

In order to use the Groq API you need to make sure you are using python 3.8 and that you add the Groq python libraries to your path. For python 3.8 you can either use the installed system python3.8 or use conda to install python3.8. 

### System python3.8
You need to fully quantify the path to python since Ubuntu 22.04 defaults to python3.10. This means you need to use
```bash
/usr/bin/python3.8
```

Then to install jupyter notebook in your home directory, you would need to do
```bash
/usr/bin/python3.8 -m pip install --user jupyter
```

### Conda
First install miniconda by following [Conda Installation Guide](conda-and-spack-installation.md#installing-conda).
Then create a groq environment with 
```bash
conda create -n groqflow python=3.8.13
conda activate groqflow
```
See the [GroqFlow Installation](https://github.com/groq/groqflow/blob/main/docs/install.md) for more details for setting up the Conda environment.

## Graphical Access to Groq Systems
See [ThinLinc Quickstart](ThinLinc.md).

## Jupyter Notebooks
See [Jupyter Notebook Quickstart](jupyter-quick-start.md) for more information on setting up Jupyter Notebooks within ExCL.

## Getting started Resources
- [Groq API Tutorials](https://github.com/groq/GroqAPI/tree/main/gapi/tutorials)
- [GroqFlow Getting Started](https://github.com/groq/groqflow#getting-started)

## Useful Groq Commands
- Run regression tests to verify card functionality: `/opt/groq/runtime/site-packages/bin/tsp-regression run` 
- Get Groq device status: `/opt/groq/runtime/site-packages/bin/tsp-ctl status` 
- Monitor temperature and power: `/opt/groq/runtime/site-packages/bin/tsp-ctl monitor`
