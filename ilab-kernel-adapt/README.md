# ILAB Kernel and Environment

## Summary

The ADAPT JupyterHub has a dedicated environment and kernel for the ILAB.
The environment has all of the JupyterLab dependencies, including the backend
extensions. The kernel has all of the packages, including application dependencies.

Ideally, we want to keep both seperate. If changes are required to support a new notebook,
new packages should be installed on the kernel, and not on the environment. The environment
should only keep the packages necessary to serve the JupyterLab ecosystem. This way, we minimize
dependency resolution problems, and downtime to fix environment problems.

## Important Concepts

- Environment and kernel structure:

```bash
/gpfsm/ccds01/home/appmgr/app/jupyterhub/ilab
├── backup
├── env
├── jupyter_ilab
└── kernel
```

From the given tree:
- backup: backup directory to store environment state
- env: environment directory for JupyterLab dependencies
- jupyter_ilab: JupyterLab package
- kernel: kernel directory for application dependencies

## How to backup the environment and kernel

Before installing anything on the environment or kernel, we need to backup the respective
one to be able to recover from broken dependencies. The following steps outline what is required to do so.

1. Load the anaconda module

```bash
module load anaconda
```

2. Load and backup the anaconda kernel or environment you need to backup.

Backing up Environment

```bash
conda activate /gpfsm/ccds01/home/appmgr/app/jupyterhub/ilab/env
conda list --explicit > "/gpfsm/ccds01/home/appmgr/app/jupyterhub/ilab/backup/env-"`date +"%Y-%m-%d.out"`
```

Backing up Kernel

```bash
conda activate /gpfsm/ccds01/home/appmgr/app/jupyterhub/ilab/kernel
conda list --explicit > "/gpfsm/ccds01/home/appmgr/app/jupyterhub/ilab/backup/kernel-"`date +"%Y-%m-%d.out"`
```

## How to Install Packages into the Kernel

1. Load the anaconda module

```bash
module load anaconda
```

2. Load and backup the anaconda kernel.

```bash
conda activate /gpfsm/ccds01/home/appmgr/app/jupyterhub/ilab/kernel
conda list --explicit > "/gpfsm/ccds01/home/appmgr/app/jupyterhub/ilab/backup/kernel-"`date +"%Y-%m-%d.out"`
```

3. Install the packages.

```bash
conda install -c conda-forge ipysheet
```

## How to Install Extensions

An example on how to install an extension is listed below.

```bash
jupyter labextension install dask-labextension
jupyter serverextension enable --py --sys-prefix dask_labextension
```

## Recovering an Environment

Worst case scenario, the environment is broken and we need to revert it back to the previous
state. We can recover from the backup file created with the following:

```bash
conda create --file /gpfsm/ccds01/home/appmgr/app/jupyterhub/ilab/backup/$backup_filename -n my_new_environment
```
