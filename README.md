## Use pip and Conda to make your software easy to install for everyone and reach a larger audience!

In this tutorial, you will learn how to make your existing tool pip and conda installable. Go ahead and start with cloning this repository:

`` git clone https://github.com/balabanmetin/pip-conda-tutorial-diameter.git``

`` cd pip-conda-tutorial-diameter``

Next, install the dependency packages for this tutorial using pip. Make sure your Python distribution has `pip` and `conda` installed:

``pip install twine setuptools``

The application we are creating is [nw_diameter](nw_diameter). It is a simple script that takes a newick file as an input and computes its diameter (a.k.a. the largest pairwise tree distance within the tree).


### Pip tutorial 

In order to upload you project to PyPi (where pip packages are stored), you must create a PyPi account first using the following link:

[PyPi Register](https://pypi.org/account/register/)

Once the account is ready, you must create a [setup.py](setup.py) file. Go ahead and edit this file. You must change the package name (`name` field) since I already reserved the name `'tutorial-diameter'` for this tutorial ;)

`setup.py` is ready. Next we create a distribution archive by running the following command inside the repository directory:

`python setup.py sdist`

This creates a `tar.gz` file in a new directory `dist`. Final step is to upload this archive into PyPi servers using `twine`

`twine upload dist/*`

Type in the username and password of your PyPi account, and your package is now live!. Let's test it. Change to the `data` directory.

`cd data`

Install your package using pip. Since I named my package as `tutorial-diameter`, I install it using the following command:

`pip install tutorial-diameter`

If everything went well, run the command `nw_diameter` using the test newick file:

`nw_diameter data/tree.nwk`

Diameter of this tree is 0.7!.

### Conda tutorial
#### Using PyPi skeleton
If you have already built and uploaded your package to PyPi, you can use it as a skeleton to make the Conda build easier.

`conda skeleton pypi tutorial-diameter`

Now you should see the directory `tutorial-diameter` created for you, inside which you can see the file `meta.yaml`. This is the recipe needed to build a conda package. Now execute the following command to build:

`conda build tutorial-diameter`

To upload to Anaconda cloud, run the following command:

`anaconda upload $HOME/anaconda3/conda-bld/<YOUR_OS>/tutorial-diameter-1.0.1-py38_0.tar.bz2`

#### Using Github
If you do not have a PyPi package, you can build a Conda package directly from your code on Github. To do so, change the `source` section of your `meta.yaml` to:

git_rev: main
git_url: https://github.com/balabanmetin/pip-conda-tutorial-diameter.git


