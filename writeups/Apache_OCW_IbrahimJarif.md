# How to contribute to Apache Open Climate Workbench

## What is Apache Open Climate Workbench (OCW)

Apache Open Climate Workbench is an effort to develop software that performs climate model evaluation using model outputs from a variety of different sources the [Earth System Grid Federation](http://esgf.llnl.gov/), the [Coordinated Regional Climate Downscaling Experiment](http://www.cordex.org/), the [U.S. National Climate Assessment](http://nca2014.globalchange.gov/) and the [North American Regional Climate Change Assessment Program](http://www.narccap.ucar.edu/) and temporal/spatial scales with remote sensing data from [NASA](http://www.nasa.gov/), [NOAA](http://www.noaa.gov/) and other agencies. The toolkit includes capabilities for rebinning, metrics computation and visualization.

## Getting Involved
You don't need to be a software developer to contribute to Apache Open Climate Workbench! To be successful the community requires (and appreciates) a range of different skills, levels of involvement and degrees of technical competency.

So, if you want to get involved in Apache Open Climate Workbench, there is almost certainly a role for you. We are looking for people to:

* Provide feedback
* Write or update documentation
* Help new users
* Recommend the project to others
* Test the code and report bugs
* Fix bugs and submit patches
* Give us feedback on required features
* Write and update the software
* Create artwork
* Translate to different languages
* Anything you can see that needs doing

All of these contributions help to keep a project active and strengthen the community. The [project team](https://climate.apache.org/community/people.html) and the broader community will therefore welcome and encourage participation, and attempt to make it as easy as possible for people to get involved

## Setting up development environment

### Grab the latest code from the ASF (User)
```
git clone http://git-wip-us.apache.org/repos/asf/climate.git
```
### Dependency Installation
#### Using conda
This is the simplest and recommended installation method. You will first need to install the conda package manager, which can be readily obtained through either the [Anaconda](https://store.continuum.io/cshop/anaconda) or [Miniconda](http://conda.pydata.org/miniconda.html) scientific python distributions. Be sure to allow the installation to update your PATH for you. 

Before invoking conda to install the dependencies, it's always a good idea to ensure that your version of conda is up to date. You can do this with:
```
# Update conda packages
$ conda update conda
# Add the conda-forge repository to your package manager
$ conda config --add channels conda-forge
# Install ocw to ~/anaconda or ~/miniconda2/3
$ conda install ocw
```

This installation method should work for all major platforms, making it particularly advantageous.

### Test Your Installation
The easiest way to test your installation is to run one of the example scripts in `$HOME/climate/examples`.
```
$ cd $HOME/climate/examples
$ python simple_model_to_model_bias.py
```
If you face run-time exceptions with the above, make sure you have the [libpng16](http://sourceforge.net/projects/libpng/files/libpng16/) library [installed](http://geeksww.com/tutorials/libraries/libpng/installation/installing_libpng_on_ubuntu_linux.php), and are not running libpng12.

If everything runs successfully you should see a plot similar to the one below in the examples folder.
![](https://cwiki.apache.org/confluence/download/attachments/40507990/wrf_bias_compared_to_knmi.png?version=1&modificationDate=1427403747000&api=v2)

## Installing the OCW UI
If you would like to install and use the OCW-UI for running simple evaluations through your web browser, check the [Open Climate Workbench User Interface Installation and Overview](https://cwiki.apache.org/confluence/display/CLIMATE/Open+Climate+Workbench+User+Interface+Installation+and+Overview) guide to get started.


## Using the OCW VM
If you want to get up and running with OCW quickly and with minimal overhead consider using the OCW VM. You can read about how to build the VM on the [OCW VM - A Self Contained OCW Environment](https://cwiki.apache.org/confluence/display/CLIMATE/OCW+VM+-+A+Self+Contained+OCW+Environment) page. The OCW VM gives you an isolated VM environment with OCW pre-setup for you so you can get up and running without installing dependencies or configuring your system. 

## Mailing lists
This is where the community hangs out and discussion about development happens. This list is used to coordinate activities and ensure we are all pulling in the same direction.

* Subscribe: dev-subscribe@climate.apache.org
* Post (after subscription): dev@climate.apache.org
* Unsubscribe: dev-unsubscribe@climate.apache.org
* Apache Archives: [Climate Dev Mail Archives](http://mail-archives.apache.org/mod_mbox/incubator-climate-dev/) (non-searchable)
* The Mail Archive Archives: [Climate Dev Mail Archives](http://www.mail-archive.com/dev%40climate.apache.org/) (searchable)

## Useful Links
* Project Website - https://climate.apache.org/
* Project Source Code - https://github.com/apache/climate
* Documentation - https://cwiki.apache.org/confluence/display/CLIMATE/Home
* Python API Docs - https://climate.apache.org/api/current/index.html
* Issue Tracker - https://issues.apache.org/jira/browse/climate