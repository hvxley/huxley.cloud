---
layout: ../../layouts/MarkdownPostLayout.astro
title: 'Installing Pulsar on Ubuntu 22.04'
pubDate: 2023-06-09
description: 'Pulsar is a community-led text editor that I welcome you to enjoy.'
author: 'Cloud Huxley'
image:
    url: '/img/blog/pulsar_screengrab.png'
    alt: 'Pulsar screengrab'
tags: ["ubuntu", "development"]
---

### Installing Pulsar on Ubuntu 22.04

#### Background
Ages ago, I fell in love with Atom text editor, which was created by [Github](https://github.com) in 2014. In June of 2022, Github announced that atom was reaching its end of life for development and support “in order to prioritize technologies that enable the future of software development”.

On December 15, 2022 Pulsar-edit was born as a beta release.  The goal was to continue the development of the original Atom project so that access to third-party plugins and themes could still be achieved.

#### Is Pulsar the End-All-Be-All?
Not even close. Wikipedia offers up a [comparison of various text editors](https://en.wikipedia.org/wiki/Comparison_of_text_editors), and then there are lists of IDEs to consider. An Integrated Development Environment (IDE) includes a compiler, debugger and related components, as well as a text editor, for software developers to ease their work flow. I don’t do much compiling because of my choices in technology stacks, so an amped-up text editor with debugging and add-on components is good enough for me. As such, I’ve modeled my articles after the tools that work for me.

#### So Let’s Get To It
In the following steps, we will evaluate several methods for installing Pulsar.
First, let's install `wget`
```bash
$ sudo apt update
```
```bash
$ sudo apt install wget -y
```

##### 1. .deb Package
In the terminal enter the following commands
```bash
$ wget https://github.com/pulsar-edit/pulsar/releases/download/v1.101.0-beta/Linux.pulsar_1.101.0-beta_amd64.deb
```
```bash
$ sudo dpkg -i Linux.pulsar_1.101.0-beta_amd64.deb
```

Finally, test your installation by opening up your current directory in pulsar.
```bash
$ pulsar .
```

If everything looks good, you should have Pulsar ready to operate.

##### 2. AppImage
Download the AppImage file from the following location
```bash
$ wget https://github.com/pulsar-edit/pulsar/releases/download/v1.101.0-beta/Linux.Pulsar-1.101.0-beta.AppImage
```
`chmod` to allow the execution of the AppImage
```bash
$ sudo chmod +x Linux.Pulsar-1.101.0-beta.AppImage
```

Run the AppImage from the download location
```bash
$ ./Linux.Pulsar-1.101.0-beta.AppImage
```

That’s all there is to it. With an AppImage, there is nothing to install or uninstall. Everything is self-contained within the AppImage file.

##### 3. From a Compressed .tar.gz File
Download the `.tar.gz` file from the official website
```bash
$ wget -c https://github.com/pulsar-edit/pulsar/releases/download/v1.101.0-beta/Linux.pulsar-1.101.0-beta.tar.gz -O - | tar -xz
```
`cd` into the pulsar directory
```bash
$ cd pulsar-1.101.0-beta
```
Copy the current directory to `/opt/pulsar` so we remember where our files are stored.
```bash
$ sudo cp -R . /opt/pulsar
```
Create a symbolic link for the the pulsar executable in /usr/bin/
```bash
$ sudo ln -s /opt/pulsar/pulsar /usr/bin/pulsar
```
Check the version and exist to verify everything installed correctly.
```bash
$ pulsar -v
```

#### Uninstalling Pulsar
To uninstall Pulsar from the debian package, simply run the following
```bash
$ sudo dpkg -P pulsar
```

To uninstall Pulsar from the .tar.gz file, simply delete the file directory and symbolic link
```bash
$ sudo rm -rf /opt/pulsar && sudo rm /usr/bin/pulsar
```

#### Wrapping Up
We learned a few different ways to install Pulsar in this article.  Needless to say, I really enjoy using it. I hope you do as well.
