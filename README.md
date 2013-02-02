This repository contains definitions and files necessary for recreating vagrant boxes suitable for running module tests with.

The primary goal is to create boxes that have very little specialisation at this level, the standard veewee templates should be very rarely modified to keep it simple.

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

    <osdistro>-<derivative>-<version>-<arch>

* osdistro: for example: centos, ubuntu, windows
* derivative: (optiona) server, desktop
* version: 8, 2008, 1104
* arch: x64, i386

Examples:

    ubuntu-server-1104-x64
    centos-58-i386
    windows-2008r2-x64

Naming caveats:

* The name becomes the hostname of the box ... so you have to be careful.
* Debian/Ubuntu doesn't like underscores in the name.
* A dot in the box name would create a subdomain, which is probably not desirable.
