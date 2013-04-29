This repository contains definitions and files necessary for recreating vagrant boxes suitable for running module tests with.

You can access to the produced vagrant boxes here:

<a href="http://puppet-vagrant-boxes.puppetlabs.com">http://puppet-vagrant-boxes.puppetlabs.com</a>

The primary goal is to create boxes that have very little specialisation at this level, the standard veewee templates should be very rarely modified to keep it simple, and even then bug fix should always be feed back to upstream (ie. VeeWee). This holds for any bugs we find in the templates, and any new templates that are required. In short our goal here is not to fork VeeWee templates, but to provide a snapshot of the template at box build/publish time.

## Environment setup

You'll need Ruby 1.9.3 and Bundler before you begin. You should also install a copy of Vagrant from the instructions provided here:

<http://downloads.vagrantup.com/>

Once you have vagrant installed, start by entering the directory where you have cloned this project:

    $ cd <path to repo>

*Optional* Create an RVM gemset:

    $ rvm --create --ruby-version use ruby-1.9.3@puppet-vagrant-boxes

Then install the bundle:

    $ bundle install

## Adding a new definition

Note: Change the base command between vbox or fusion depending on your target provider.

Get a list of available definitions:

    $ veewee [vbox|fusion] templates

Pick one, and define it using:

    $ veewee [vbox|fusion] vbox define '<box_name>' '<template_name>'

Make sure <box_name> follows the convention:

    <osdistro>-<derivative>-<version>-<arch>-<virtual-type>-<variant>

* osdistro: for example: centos, ubuntu, windows
* derivative: (optional) 
    * for ubuntu: svr, dtop (used to be server, desktop)
* version: 8, 2008, 1104
* arch: x64, i386
* virtual-type: type & version.
    * vbXXXX: virtualbox + version (used to be vboxXXX)
    * vfXXX: vmware fusion + version (used to be fusionXXX)
* variant (optional):
    * nocm: designates no configuration management tools were loaded

Examples:

    ubuntu-svr-1104-x64-vb4210
    centos-58-i386-vb4210
    windows-2008r2-x64-vb4210
    debian-607-x64-vb4210-nocm
    centos-64-x64-vf503

### Naming caveats

NOTE: There are reasons why we name things thusly, if you don't care skip this section.

You are probably wondering why we have the strictish naming conventions, I assure you its not by choice, there are limitations in the naming that we are working around:

* The name becomes the hostname of the box ... so you have to be careful what you use. Later on in vagrant one should normally change the hostname themselves, but we can't rely on our users doing this so we have to get it right.
* Debian/Ubuntu doesn't like underscores in the hostname of a box. So we avoid this.
* A dot in the box name would create a subdomain, which is probably not desirable. This is why we munge versions into 1 string of digits instead of dot delimiting them.
* There is a weird bug in Ubuntu 12.04.2 (can't replicate in 10.04) whereby hostnames that are too long will not boot in vagrant. I've found hostnames shorter than 37 chars should work fine. No idea why ...

## Updating index.html

Once you've produced a new box you should modify html/index.html to add it so it can be accessed from the index on S3.

## Building a box

Finally, follow the next steps for building a box.

Pick a box to build:

    $ veewee [vbox|fusion] list

To build it:

    $ veewee [vbox|fusion] build <box-name>

At this point it will download necessary ISO's and start building a box.

Now validate the box:

    $ veewee [vbox|fusion] validate <box-name>

And export the vm to a .box file:

    $ veewee [vbox|fusion] export 'centos-58-x64'

## Publishing to S3

Now upload the box located in the current directory (ie. `centos-58-x86_64.box`) to the S3 bucket `puppet-vagrant-boxes`, and if you modified the index.html, upload that as well.

## Publishing to vagrantbox.es

If the image is new, or you changed the name, also update the site http://vagrantbox.es/, you do this by raising a PR on the repository below:

<http://github.com/garethr/vagrantboxes-heroku>
