# How to contribute to WikiToLearn? 

## What is WikiToLearn? 

WikiToLearn is a portal that aims to create free collaborative and readily accessible textbooks. Our philosophy can be summarized as *"Knowledge only grows if shared"*. On this platform, teaching and studying merges into the cooperative writing and revision of notes and textbooks, which can then be organized and reassembled, according to each user's needs.

## Why is it an innovation?

WikiToLearn does not bring new knowledge. WikiToLearn offers a new approach to knowledge: it rediscovers and proposes again the attitude, now almost forgotten by mankind: the collaboration and communication among thinkers. This philosophy is the one that led our civilization to take the huge steps that have brought us here today, with our endless heritage of knowledge. Without the collaboration and the communication among thinkers, without the free availability of knowledge, no big discovery would have been possible. This is what we are trying to restore. We are moved by the love for free knowledge, owned by no one and accessible to everyone. In collaboration (without any kind of remuneration), we want to make this vision possible. Open source in this context gains a profound and significant meaning, merging naturally with our philosophy. Here are the basics:

* Any content can be modified. This leads to a continuous development of the existing material, to this philosophy of *collaboration* and *communication* among thinkers.
* Everything on WikiToLearn is freely accessible and downloadable. In this way, knowledge is made available to everyone.

## How can I contribute?
 
WikiToLearn is actively developed both on the technical and the content side. It's possible to contribute in several ways, regardless of the user's skills and experience.

### Translation
Are you fluent in (at least) two languages? 
Translating on WikiToLearn is an opportunity to practice your translation skills, at the same time you will learn about new things, and you will contribute to the growth of knowledge in the world . The content does not need to be written from scratch, the translation into several languages is as important as the content itself, to guarantee its accessibility to everyone.

If you want to help with translation you can join the [#translation](https://chat.wikitolearn.org) channel.

### Web development
WikiToLearn is a project based on MediaWiki, so we always need developers to fix bugs and develop new innovative programs. Web development is split into groups and every group has its maintainer. If you want to help with tech you can join the [#tech](https://chat.wikitolearn.org) channel.

### Setting up local WikiToLearn instance with WikiToLearnHome

#### Requirements
* 64-Bit Computer (docker need a 64 bit system)
* GNU/Linux with docker or Windows/OSX with virtualization compatability and enabled
* Stable internet connection (download size can be up to 10 GB)

This procedure may fail if you have no Internet access or if the connection is filtered by firewall – this could happen in public places such as universities, libraries, airports, etc.

#### GNU/Linux installation
##### Prerequisites
WTL and WTLH have some dependecies:

* any version
    * curl
    * rsync
    * dirname
    * realpath
    * git
    * pandoc
    
* specific version required
    * docker ( >= 1.10.3)
    * python3
    
##### Ubuntu/Debian prerequisites install
```sudo apt-get install curl rsync coreutils realpath git python3 pandoc```

##### Arch prerequisites install
```sudo pacman -Sy curl rsync coreutils git python3 pandoc```

`realpath` is in `AUR`

#### Docker installation
Docker is a quickly evolving technology, and it may be possible that the your distro official repository do not have yet the docker version requierd to run WTL. We thus recommend to install docker following the [official guide](https://docs.docker.com/engine/installation/).

Do not forget to add your user to the docker group, so that you do not have to use super user privileges every time you have to manage docker images and volumes. WTLH is intended to work only if your user is added to docker group, otherwise you get errors related to missing the correct permissions since WTLH is not intended to be executed with super user rights.

#### Pandoc
Pandoc is used to convert markdown documentation into mediawiki, that can be imported to [meta](https://meta.wikitolearn.org/Main_Page), thus this is not a real prerequisite, it is only needed if you are willing to help us keeping our online documentation up to date!

Now you can proceed to the actual download with the following command line:

`git clone --recursive https://github.com/WikiToLearn/WikiToLearnHome.git`

This creates a folder called WikiToLearnHome (inside your home directory) which contains all the necessary files. This folder contains all script used to manage the WikiToLearn instance.

Before the download of all the code you have to generate a [GitHub token](https://github.com/settings/tokens) (leave all the scopes unchecked) (used for composer).

`cd WikiToLearnHome
./create-config.sh -t <github token>`

We recommend using SSH to communicate with github ([guide on ssh key generation here](https://help.github.com/articles/connecting-to-github-with-ssh/)).

After this setup you can download the WikiToLearn repository using this script

`./instance.sh download`

##### Start and stop the server

To start the local server the command is

`./instance.sh first-run`

Now you can work on your local instance of WikiToLearn and see your work on www.tuttorotto.biz

You can shutdown the server with

`./instance.sh stop`

And start again with

`./instance.sh start`

Sometimes you might want to wipe out the server and for this you can use

`./instance.sh delete`

Read the guide to [instance.sh](http://meta.wikitolearn.org/WikiToLearn_Home/WikitoLearn_Home_Documentation/Instance_Doc) for a deatailed description of how to use WTLH to manage the WTL instance.


##### Change the config and restart the dockers

You can also change the configuration of the environment (for example changing the number of mathois workers) and restart the containers without re-pulling all the images.

Stop the running instance, if you have any.

`./instance.sh stop`

Change the configuration:

`nano ./create-config.sh`

Create the configuration files and update the scripts with the new parameters

`./create-config.sh -t <github token> -p <protocol> --existing-repo --force-new-config
./instance.sh create`

Start the new instance (with the new parameters)

`./instance.sh start`

#### Vagrant Installation for Windows/OSX

WTL is build to work on GNU/Linux. It uses GNU/Linux software, enclosed inside docker containers, that require the GNU/Linux kernel. Hence, if you want to develop WTL from a Windows/OSX environment you need to install a virtual linux system. We remind yout in order do use a virtualization software, you have to enable virtalization in your BIOS, as [explained in this page](http://meta.wikitolearn.org/WikiToLearn_Home/WikitoLearn_Home_Documentation/Local_WikiToLearn_Instance/How_To_Enable_Virtualization_On_Your_PC).

##### Vagrant Installation
Using Vagrant is a quite simple way of using a virtual linux system for development purposes.

This procedure requires using port 8080 tcp, 3128 tcp, 2121 to 2221 tcp on your host, this shouldn't be a problem unless you are running a network server (apache2, remote web control, ecc.).

If you have a **Windows/OSX** operating system, then you need to run a WikiToLearn instance using Vagrant. You can also install Vagrant if you have a Linux o.s. However, it is not required to get a fully working installation. You can just skip to the next step.

First, you need to install:

* [VirtualBox](https://www.virtualbox.org/wiki/Downloads/) as engine for vagrant
* [Vagrant](https://www.vagrantup.com/docs/installation/) for Windows/OS X users, for Linux it's optional. On Windows require restart.

Now you have to download the last [devvagrant](https://github.com/WikiToLearn/devvagrant). You can download a snapshot as zip and then unzip it in your directory or use “git clone” to clone the repo.

Now you have to

`cd devvagrant # Where there is the Vagrantfile
vagrant up`

This can take a while because it will download the VM.

And then log in to the shell with vagrant command

`vagrant ssh`

The machine has a FTP server to simplify file transfer, the server is anonymous and is reachable with 127.0.0.1 address at 2121 port.You have to configure your browser to get proxy configuration file from http://127.0.0.1:8080. To configure it on Mac OS X, go to System Preferences -> Network -> Advanced -> Proxy -> Automatic Proxy Configuration and write http://127.0.0.1:8080 as URL.

Once you set up everything, you can proceed following the Linux Installation Guide, starting from cloning the git repo.

## Conclusion

If you have specific questions, want to share your experience/problems you are facing during contributing or just want to say hi - feel free to DM me (@srijancse) or anyone available on the [chat.wikitolearn.org](https://chat.wikitolearn.org) :)





