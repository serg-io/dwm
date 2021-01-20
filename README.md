## Description ##

This repository is a fork of the Suckless [dwm](https://dwm.suckless.org/) (dynamic window manager)
project and was created to manage patches. To avoid any conflicts with the original _master_ branch
from dwm, this repository does not contain a _master_ branch. Instead, it has a _main_ branch which
contains a [PKGBUILD](https://wiki.archlinux.org/index.php/PKGBUILD) file that makes it easy to
install a patched version of dwm in [Arch Linux](https://www.archlinux.org/). All patches are stored
seperately in branches with names that start with "patch-".

## Getting Started ##

To get started, clone this repository and rename the default `origin` remote.

	git clone git@github.com:serg-io/dwm.git
	cd dwm
	git remote rename origin github

Now add a remote for the original `suckless` repository.

	git remote add suckless https://git.suckless.org/dwm

## Installation ##

To install a patched version of dwm in Arch Linux first make sure you have all the latest changes
from the `suckless` repository.

	git fetch suckless

Create a `build` branch using `suckless/master` as a starting point and merge the `github/main`
branch.

	git branch --no-track build suckless/master
	git checkout build
	git merge github/main

If you already have a `build` branch reset its `HEAD` and merge `github/main`.

	git checkout build
	git reset --hard suckless/master
	git merge github/main

Now that you have a `build` branch with the files from `github/main` you can use
[makepkg](https://wiki.archlinux.org/index.php/Makepkg) to build and install dwm.

	makepkg -sci

Before dwm is built, the `PKGBUILD` script will merge all the remote branches that start with
"patch-".

## Patch Branches ##

If you fork this repo, and use your own forked repo instead of this one, you'll be able to create
your own patch branches. To create a patch branch, you must first fetch the most recent changes
from `suckeless`.

	git fetch suckless

Then create a new branch using `suckless/master` as the starting point and push it to your
repo. Make sure the name of the branch starts with "patch-". The
[noborder](https://dwm.suckless.org/patches/noborder/) patch will be used for this example.

	git branch --no-track patch-noborder suckless/master
	git push -u github patch-noborder
	git checkout patch-noborder

Download and apply the required patches. In this case,
[dwm-noborder-6.2.diff](https://dwm.suckless.org/patches/noborder/dwm-noborder-6.2.diff) is the
only required patch file.

	git apply dwm-noborder-6.2.diff

Commit and push your changes.

	git add .
	git commit -m "dwm-noborder"
	git push

You can now follow the installation instructions explained above and your patch branch will be
automatically merged during the installation.