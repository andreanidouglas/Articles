---
title: The new kid in town: Fedora Silverblue!
published: true
description: What is Fedora Silverblue and why has the potential to be your next os.
tags: Linux, Fedora, Silverblue, Operating Systems
---

On April 30th, 2019 the [Fedora Project](https://getfedora.org/) released version 30 of its Linux distribution.

After the acquisition by IBM, Fedora is no longer maintained by Red Had, it's now a complete community-based Distribution based on the **4 Foundations** (Freedom, Friends, Features, and First).

For this release also, Fedora delivered 3 additional _emerging_ to complete its lineup:

* Fedora CoreOS (minimal container focus distro)
* Fedora IoT (OSS platform for IoT infrastructure)
* Fedora Silverblue (Immutable workstation based on container workflows)

On this article, I will cover the last, but let me know in the comments and we can discuss the other two as well.

## Overall

![silverblue](https://docs.fedoraproject.org/en-US/fedora-silverblue/_images/silverblue-logo.svg)

Silverblue is a new concept on the linux distribution. As described earlier is an immutable operating system. As is, it aims to be a powerful, stable and reliable platform for developers and professionals alike.

Being immutable means that each and every installation will be exactly the same, being easier to develop and test making it less prone to bugs. But it also means that changes in the structures of the OS are not allowed by the user.

![immutable](http://abhirockzz.files.wordpress.com/2014/01/immutable-defined.png)

The userland experience will be a bit different from a standard Linux distro though. At first glance, you will have your normal Gnome environment and the **Applications Store** will have most of the familiar application you need. They will work as regular applications besides the fact that they will not be installed directly to the OS. Each application will live in a sandbox environment called Flatpak.

For developers the name of the game is containerization. Silverblue provides lots of functionality to create and deploy containers for all your projects.

![containers](https://www.marineinsight.com/wp-content/uploads/2011/05/Container-lashing-with-rods.jpg)

## Using Silverblue

Installing Fedora Silverblue is as easy as normal Fedora workstation, just download the image from the main website [silverblue.fedoraproject.org](https://silverblue.fedoraproject.org/), create a bootable flash drive (you can user Etcher for this) and follow the instructions prompts.

On your first login, you will be greeted by a nice Gnome environment, like many other Distros. If available, it will start to download any available updates for the current environment and will prompt you to install them once finished.



These downloads are a new version of pieces of software, but more important OS updates. These updates are released officially by the maintainers' group and can be check with the command `$ rpm-ostree status`. 

To force the download of new releases just issue `$ rpm-ostree update` (every update requires a reboot of the workstation). If any upgrade manages to break your OS or any functionality simply rollback to a previous state `$ rpm-ostree rollback`.

The software can be acquired by the **Software Center** (read this [link](https://docs.fedoraproject.org/en-US/fedora-silverblue/getting-started/) to add more repositories to the list).

For developers, the most important feature is the **Toolbox**:

Toolboxes are container-based development environments where you can create and explore without damaging the base system. A simple container can be created by entering `# toolbox create --container=<container_name>`.

This will download an up-to-date image of a minimum fedora container, issue `# toolbox enter --container=<container_name>` to enter a shell session within it. From here, you can treat it as a normal Fedora Workstation distro, the command `dnf` will be your friend to download any necessary packages (e.g. `$ dnf install python3.7`)

## Conclusion

![conclusion](https://cdn1.iconfinder.com/data/icons/got-idea-vol-2/128/assumption-512.png)

So, what are your thoughts about this new approach? Do you see yourself leveraging any of the features of Silverblue? My laptop already has Silverblue installed and ready to use, a static immutable OS is a great idea. No more messing up with kernel versions or dealing with multiple versions of the same software (e.g python2.7 vs python3.7).
