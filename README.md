# ilab-jh-management

Repository to document ILAB JH Management

## Summary

The ILAB develops many JH Notebooks between the ADAPT and SMCE environments.
This repository attempts to document the steps required to perform some of these
management things including a CHANGELOG of changes.

The ADAPT environment is a simple anaconda environment with extensions installed at
the environment level, and packages installed at the kernel level.

The SMCE environment is a Docker container with the extensions installed at the container
level, and packages installed at the kernel level (storage-based anaconda).

## Requirements

TBD

## TODO

- We should explore the use of Mamba as the package manager for our environments. Mamba offers
faster environment solving and better support for packages.

## References

- [Anaconda](https://www.anaconda.com/)
- [Mamba](https://github.com/mamba-org/mamba)
