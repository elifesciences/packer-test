
# About

This repo contains the scripts required to use `packer` to build an AMI and a local vagrant box for virtual box, configured with the core
environment for hosting the eLife Drupal journal site. 


# Building an AMI

Modify `aws-variables-example.json`, add in your secret and your key.
Optionally rename to `aws-variable.json`, then for a givne json configuration file run

	$ packer build -var-file=aws-variables.json config.json 

If you are using the fish shell a convinience script is provided, just run

	$ fish build-packer-aws.fish config.json

For example, 
	$  fish build-packer-aws.fish elife-base-ami.json 

will build a base AMI on top of `ami-de0d9eb7`, and will then install `vim` and `curl`.

	$ fish build-packer-aws.fish elife-drupal-base-ami.json

Will build an AMI configured with the cookbooks specified in elife-drupal-base-ami.json.



# Building a vagrant box

Download `ubuntu-12.04.3-server-amd64.iso`, for example from [here](http://releases.ubuntu.com/precise/). Verify that the md5 is correct,
update the path to the iso image in `ubuntu-64.json`, then:

	$ packer build ubuntu-64.json 


This will use the packer post-processor to create a clean vagrant box that installs in virutalbox. This box is 
built on top of ubuntu server 64.

To use the Vagrantfile provided with this repo do the following:

	$ vagrant box add packer1 packer_virtualbox_virtualbox.box 
	$ vagrant up 

You can then `ssh` into your clean box with 
	$ vagrant ssh

Password is `vagrant`

