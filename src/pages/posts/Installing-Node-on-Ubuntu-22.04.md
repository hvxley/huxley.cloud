---
layout: ../../layouts/MarkdownPostLayout.astro
title: 'Installing Node.js on Ubuntu 22.04 Jammy Jellyfish'
pubDate: 2023-06-10
description: 'A brief tutorial on installing the NodeJS environment.'
author: 'Cloud Huxley'
image:
    url: '/img/blog/node_stats.png'
    alt: 'Node stats'
tags: ["nodejs", "node", "ubuntu"]
---
### Installing Node.js. on Ubuntu 22.04 Jammy Jellyfish

The following article is for testing purposes only. This code was developed to help you understand the pieces required to install NodeJS.

#### What is Node?
Node is a JavaScript runtime engine for server-side programming that allows developers to create a back-end using the same language traditionally used in Browser-based scripting. Node also comes with a packaging system, so you can choose which packages to include in your project. Packages can be found all over, but some places for beginners include [NPMjs.com](https://www.npmjs.com/) and [Github](https://github.com/).

#### Is Node right for your project?
I would imagine, yes. If you’re looking to have your project contained in a file directory (as most projects are) then we’re off to a good start. If you’re taking on a project that contains a `package.json` file, Node is a part of that project already.

#### 1. Install with Apt Package Manager
Installing Node through apt is the easiest approach, but you are left with a version of Node that has been dated, and is on the way out.

Start by refreshing your package index
```bash
$ sudo apt update
```

Next, install Node
```bash
$ sudo apt install nodejs npm
```

After installation, check your node and NPM versions
```bash
$ node -v && npm -v
```

That’s all there is to it with APT!

#### 2. Install with Snap Package Manager
Snap packages have been built into Ubuntu, and as it turns out, they host a newer version of Node than we would find in the Apt repository. To install Node, run
```bash
$ sudo snap install node --classic
```

#### 3. Install with Apt using a NodeSource PPA
Installling Node from a personal package archive (PPA) is a little riskier, as we should always be skeptical of third-party shell scripts, but NodeSource is a tried-and-true service, and you can certainly inspect the code before running it.

Change the directory to your user directory
```bash
$ cd ~
```

We need curl to fetch our installation script, so let’s install it using Apt
```bash
$ sudo apt install curl -y
```

Next, we’ll fetch the script. Be sure to replace 18.x with the version you want.
```bash
$ curl -sL https://deb.nodesource.com/setup_18.x -o nodesource_setup.sh
```

Run the script with sudo
```bash
$ sudo bash nodesource_setup.sh
```

The PPA will be added to your configuarion, and now we can install Node like we did in the previous step, except the NodeSource package contains both the node binary and npm, so we don’t need to install npm separately.
```bash
$ sudo apt install nodejs
```

Finally, we can check our versions to make sure everything installed correctly
```bash
$ node -v && npm -v
```

#### 4. Install from Source Code
Installing Node from source code will give you the deepest understanding of how the program works.

Download the source files from [NodeJS](https://nodejs.org/en/download/) and extract them.
```bash
$ sudo curl https://nodejs.org/dist/v18.14.0/node-v18.14.0.tar.gz | tar -xz
```

Make sure you have all of your build prerequisites installed before you begin compiling
```bash
$ sudo apt install build-essential`
```

Change into the node-v18.14.0 directory
```bash
$ cd node-v18.14.0`
```

Run the configuration
```bash
$ ./configure
```

Run make using 4 processing cores (if you have those) so we’re not waiting all day.
```bash
$ make -j4
```

Run make test
```bash
$ make test-only
```

Run make install to install Node locally
```bash
$ sudo make install
```

Export your path
```bash
$ sudo echo ‘export PATH=$PATH:/usr/local/bin’ >> ~/.profile
```

Finally, check the version of node to verify everything works
```bash
$ node -v && npm -v
```

#### Removing Node Installation
To remove Node from your system repositories, use `apt remove`
```bash
$ sudo apt remove nodejs npm
```

`apt remove` leaves configuration files behind. If you’d like to remove everything Node installed, run `apt purge`
```bash
$ sudo apt purge nodejs npm
```

To remove Node, the snap package, run `snap remove`
```bash
$ sudo snap remove node
```

To remove a source build, `cd` into the directory storing the Makefile.
```bash
$ cd node-v18.14.0
```

Run `make uninstall` to uninstall Node
```bash
$ make uninstall
```

#### Wrapping Up
We have taken away a few different techniques for both installing and
removing Node.js from the terminal of Ubuntu 22.04.
