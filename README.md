# About

This repository provides a template for [signac-flow](https://bitbucket.org/glotzer/signac-flow) projects based on the simple data management framework [signac](https://signac.readthedocs.io/).

# Documentation

The template project features the generation of a p-V phase diagram of a simulated Lennard-Jones (LJ) fluid and an ideal gas estimate.
The LJ fluid is sampled via molecular dynamics using the HOOMD-blue particle simulation toolkit.

The [signac](https://signac.readthedocs.io) data management framework itself does not enforce any specific workflow.
Basic workflow management functions are implemented in the complementary [signac-flow](https://bitbucket.org/glotzer/signac-flow) package, which provides the `FlowProject` class.
This template project is designed to streamline and demonstrate how to specialize a `FlowProject` to implement a workflow on top of a **signac** project.

Beginners should start by looking through the [signac documentation](https://signac.readthedocs.io), especially the [tutorial](https://signac.readthedocs.io/en/latest/tutorial.html).

Documentation for the template itself is in the [doc/](doc/) folder.
You can build the documentation, which contains a detailed description of all components, with:

```
$ cd doc
make html
```

# Quickstart

To get, started clone or better **fork** the repository.
All project related modules are part of the ``my_project`` package, feel free to rename it.
To execute the example workflow, follow these steps:

We start by initializing the project and a few state points with the `init.py` module.
```
python -m my_project.init 42
```
The number 42 is the random seed used for initialization, feel free to replace it with a different number or a text string, which will be converted into a numeric random seed.

The `scripts/run.py` script executes the operations defined in the `scripts/operations.py` module.
```
python scripts/run.py auto
```
The `auto` operation is a special *meta-operation*, which will execute all defined operations automatically in the right order.

We can checkout the project's status with the `status.py` module.
```
python -m my_project.status --detailed --parameters p
```
We use the ``--detailed`` flag to show the labels explicitly for each job.
The ``--parameters`` (``-p``) pargument specifies state point parameters that should be shown in the status overview.
In this case we specify to show the `p` variable, which stands for pressure.

Finally, we can analyze the data using a jupyter notebook, simply execute ``jupyter notebook`` within the project's root or `scripts/` directory and execute the `scripts/analysis.ipynb` notebook.

# Modules

The following list is a brief overview of the modules and scripts to be found within the project template.

Modules, that are usually modified by the user:

 * ``my_project/init.py`` - **Init**ialize the project and jobs
 * ``my_project/project.py`` - Configure the **project** operation flow
 * ``scripts/operations.py`` - Definition of python-based **operations**

Modules, that are usually executed by the user:

 * ``scripts/run.py`` - **Run** operations defined in the ``operations.py`` module
 * ``my_project/status.py`` - Display the project's **status**
 * ``my_project/submit.py`` - **Submit** operation(s) to a (cluster) scheduler
 * ``my_project/swith_workspace.py`` - Switch the project's **workspace**

Other modules:

  * ``my_project/environment.py`` - **Environment** definitions
  * ``my_project/util/misc.py`` - **Misc**ellaneous utility functions
  * ``my_project/util/hoomd.py`` - Various utility functions to be used with **HOOMD**-blue
  * ``my_project/util/tabulate.py`` - Functions for **table** formatting

# Merge upstream updates

To synchronize your fork with the upstream repository, follow these steps:
```
cd your_project
git remote add upstream https://github.com/glotzerlab/signac-project-template.git
git fetch upstream
```
Then either merge
```
git merge upstream/master
```
or rebase
```
git rebase upstream/master
```
to synchronize your local master branch with the upstream master branch.
