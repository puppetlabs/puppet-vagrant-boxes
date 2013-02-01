This repository contains definitions and files necessary for recreating vagrant boxes suitable for running module tests with.

## Environment setup

*Note:* You'll need Ruby 1.9.3 and Bundler before you begin.

    $ cd <path to repo>
    $ bundle install

## Rebuilding a box

Pick a box to build:

    $ veewee vbox list

The build it:

    $ veewee vbox build centos-58-x86_64

At this point it will download necessary ISO's and start building a box.

Now validate the box:

    $ veewee vbox validate 'centos-58-x86_64'

And export the vm to a .box file:

    $ vagrant basebox export 'centos-58-x86_64'

Now upload the box located in the current directory 'centos-58-x86_64.box' to the correct S3 bucket.

## Adding a new definition

Get a list of available definitions:

    $ veewee vbox templates

Pick one, and define it using:

    $ veewee vbox define '<box_name>' '<template_name>'

Make sure <box_name> follows the convention:

    <osdistro>-<version>-<arch>

* osdistro: for example: centos, ubuntu-server, windows
* version: 8, 2008, 1104
* arch: x86_64, i386
