## Plot Cheatsheet

Truncate axis 
```python
plt.ylim(1, 2)
plt.xlim(0, 1000)
```

Grid
```python
ax.grid(True, axis='y') # shows vertical lines in background
ax.grid(True, axis='x') # shows horizontal lines in background
```

Format axis
```python
from matplotlib.ticker import FuncFormatter
ax.xaxis.set_major_formatter(FuncFormatter(lambda x, pos: f'{(x ) / 10 ** 5:,.0f}x$10^5$'))
```

seaborn color 
```
Black = "#34495e"
Blue = "#3592F0"
GREEN = "#4BAD6C"
RED = "#e74c3c"
Violet = "#B148F7"
yellow = "#DEBE1F"
sns.color_palette([RED, GREEN, BLUE, BLACK])
```

custom legend
For opacity: `framealpha` 
```
plt.legend(title=legend_title, labels=[label1, label2], fontsize=14, ncol=1, title_fontsize=14, framealpha=0.8) 
```

axis and title label and font size
```
ax.set_title(title, fontsize=20)
plt.xlabel(xlabel, fontsize=16)
plt.ylabel(ylabel, fontsize=16)
ax.set_xticklabels(ax.get_xticks(), fontdict={'fontsize': 16})
ax.set_yticklabels(ax.get_yticks(), fontdict={'fontsize': 16})
```

resize the image
```
plt.tight_layout()
```

sns set background
```
sns.set(font_scale = 2, style="white" )
```




## conda cheatsheet

From [bitsurgeon](https://gist.github.com/bitsurgeon/7a2487a0ba03e37f2cc4fe1f2f2b38fb)

```sh
# check version
conda --version

# update package/conda
conda update conda
conda update <package>
conda update -n base -c defaults conda

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
conda env remove --name <env_name> 
conda remove --name <env_name> --all

# remove out-dated packages
conda clean -a

# disable conda auto-activate
conda config --set auto_activate_base false

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
