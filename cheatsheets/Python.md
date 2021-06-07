## conda cheatsheet

From [bitsurgeon](https://gist.github.com/bitsurgeon/7a2487a0ba03e37f2cc4fe1f2f2b38fb)

```sh
# check version
conda --version

# update package
conda update conda
conda update <package>

# display environment information
conda info [--envs]

# display package details
conda list
conda list -n <env_name>
conda list -n <env_name> <package>

# set or get environment setting
conda config --append channels <channel_name>
conda config --set <key> <value>
conda config --get <key>

# create environment
conda create --name <new_env_name> [package1 package2 ...]
conda create --name <new_env_name> [package==m.n]
conda create --name <new_env_name> --clone <existing_env_name>
conda create -n my_env python=3.X
 
# Add bin folder to existing conda env
conda install -n my_env python=3.X

# activate environment
conda activate <env_name>
conda activate
conda deactivate

# install package
conda search <package>
conda install <package1> [<package2=m.n> ...]
conda install package>m.n,<p.q
conda install -c <channel> <package>
conda remove -n <env_name> <package>

# environment management
conda env export > environment.yml
conda env create -f environment.yml
conda env update --file environment.yml
conda env remove --name <env_name> or conda remove --name <env_name> --all

# remove out-dated packages
conda clean -a
```

## environment.yml example

```yml
name: env_name
channels:
    - nodefaults
    - anotherchannel
dependencies:
    - package1=m.n
    - channel_name::package2>=m.n.*
    - pip:
        - package3>=m.*,<p.*
        - package4==m.n
```
## Decorators

* [Primer on python decorators](https://realpython.com/primer-on-python-decorators/)
