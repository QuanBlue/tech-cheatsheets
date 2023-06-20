<h1 align="center">
  <img src="./assets/vagrant-logo.png" alt="icon" height="150"></img>
  <br>
  <b>Vagrant Cheatsheet</b>
</h1>

<p align="center">List of the Vagrant and Vagrantfile commands.</p>

<!-- Badges -->
<p align="center">
  <a href="https://github.com/quanblue/tech-cheatsheets/graphs/contributors">
    <img src="https://img.shields.io/github/contributors/quanblue/tech-cheatsheets" alt="contributors" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/last-commit/quanblue/tech-cheatsheets" alt="last update" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/network/members">
    <img src="https://img.shields.io/github/forks/quanblue/tech-cheatsheets" alt="forks" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/stargazers">
    <img src="https://img.shields.io/github/stars/quanblue/tech-cheatsheets" alt="stars" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/issues/">
    <img src="https://img.shields.io/github/issues/quanblue/tech-cheatsheets" alt="open issues" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/blob/master/LICENSE">
    <img src="https://img.shields.io/github/license/quanblue/tech-cheatsheets.svg" alt="license" />
  </a>
</p>

<p align="center">
  <b>
      <a href="https://github.com/quanblue/tech-cheatsheets">Home page</a> •
      <a href="https://github.com/quanblue/tech-cheatsheets/tree/master/Infrastructure%20as%20Code%20(IaC)">IaC page</a>
  </b>
</p>

<br/>

<details open>
<summary><b>📖 Table of Contents</b></summary>

-  [Vagrant cheatsheet](#vagrant-cheatsheet)
   -  [Creating a VM](#creating-a-vm)
   -  [Starting a VM](#starting-a-vm)
   -  [Getting into a VM](#getting-into-a-vm)
   -  [Stopping a VM](#stopping-a-vm)
   -  [Cleaning Up a VM](#cleaning-up-a-vm)
   -  [Boxes](#boxes)
   -  [Saving Progress](#saving-progress)
   -  [Tips](#tips)
-  [Vagrantfile cheatsheet](#vagrantfile-cheatsheet)
-  [Plugins](#plugins)
-  [Credits](#credits)
</details>

> Typing `vagrant` from the command line will display a list of all available commands.
> **Note:** Be sure that you are in the same directory as the `Vagrantfile` when running these commands!

# Vagrant cheatsheet

## Creating a VM

-  `vagrant init` -- Initialize Vagrant with a Vagrantfile and ./.vagrant directory, using no specified base image. Before you can do vagrant up, you'll need to specify a base image in the Vagrantfile.
-  `vagrant init <boxpath>` -- Initialize Vagrant with a specific box. To find a box, go to the [public Vagrant box catalog](https://app.vagrantup.com/boxes/search). When you find one you like, just replace it's name with boxpath. For example, `vagrant init ubuntu/trusty64`.

## Starting a VM

-  `vagrant up` -- starts vagrant environment (also provisions only on the FIRST vagrant up)
-  `vagrant resume` -- resume a suspended machine (vagrant up works just fine for this as well)
-  `vagrant provision` -- forces reprovisioning of the vagrant machine
-  `vagrant reload` -- restarts vagrant machine, loads new Vagrantfile configuration
-  `vagrant reload --provision` -- restart the virtual machine and force provisioning

## Getting into a VM

-  `vagrant ssh` -- connects to machine via SSH
-  `vagrant ssh <boxname>` -- If you give your box a name in your Vagrantfile, you can ssh into it with boxname. Works from any directory.

## Stopping a VM

-  `vagrant halt` -- stops the vagrant machine
-  `vagrant suspend` -- suspends a virtual machine (remembers state)

## Cleaning Up a VM

-  `vagrant destroy` -- stops and deletes all traces of the vagrant machine
-  `vagrant destroy -f` -- same as above, without confirmation

## Boxes

-  `vagrant box list` -- see a list of all installed boxes on your computer
-  `vagrant box add <name> <url>` -- download a box image to your computer
-  `vagrant box outdated` -- check for updates vagrant box update
-  `vagrant box remove <name>` -- deletes a box from the machine
-  `vagrant package` -- packages a running virtualbox env in a reusable box

> **Get box:** [https://app.vagrantup.com/boxes/search](https://app.vagrantup.com/boxes/search)

## Saving Progress

-`vagrant snapshot save [options] [vm-name] <name>` -- vm-name is often `default`. Allows us to save so that we can rollback at a later time

## Tips

-  `vagrant -v` -- get the vagrant version
-  `vagrant status` -- outputs status of the vagrant machine
-  `vagrant global-status` -- outputs status of all vagrant machines
-  `vagrant global-status --prune` -- same as above, but prunes invalid entries
-  `vagrant provision --debug` -- use the debug flag to increase the verbosity of the output
-  `vagrant push` -- yes, vagrant can be configured to [deploy code](http://docs.vagrantup.com/v2/push/index.html)!
-  `vagrant up --provision | tee provision.log` -- Runs `vagrant up`, forces provisioning and logs all output to a file

# Vagrantfile cheatsheet

```ruby
Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise64"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  # config.vm.box_url = "http://domain.com/path/to/above.box"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network :forwarded_port, guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network :private_network, ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network :public_network

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider :virtualbox do |vb|
  #   # Don't boot with headless mode
  #   vb.gui = true
  #
  #   # Use VBoxManage to customize the VM. For example to change memory:
  #   vb.customize ["modifyvm", :id, "--memory", "1024"]
  # end
  #
  # View the documentation for the provider you're using for more
  # information on available options.

  # Enable provisioning with Puppet stand alone.  Puppet manifests
  # are contained in a directory path relative to this Vagrantfile.
  # You will need to create the manifests directory and a manifest in
  # the file precise64.pp in the manifests_path directory.
  #
  # An example Puppet manifest to provision the message of the day:
  #
  # # group { "puppet":
  # #   ensure => "present",
  # # }
  # #
  # # File { owner => 0, group => 0, mode => 0644 }
  # #
  # # file { '/etc/motd':
  # #   content => "Welcome to your Vagrant-built virtual machine!
  # #               Managed by Puppet.\n"
  # # }
  #
  # config.vm.provision :puppet do |puppet|
  #   puppet.manifests_path = "manifests"
  #   puppet.manifest_file  = "init.pp"
  # end

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  # config.vm.provision :chef_solo do |chef|
  #   chef.cookbooks_path = "../my-recipes/cookbooks"
  #   chef.roles_path = "../my-recipes/roles"
  #   chef.data_bags_path = "../my-recipes/data_bags"
  #   chef.add_recipe "mysql"
  #   chef.add_role "web"
  #
  #   # You may also specify custom JSON attributes:
  #   chef.json = { :mysql_password => "foo" }
  # end

  # Enable provisioning with chef server, specifying the chef server URL,
  # and the path to the validation key (relative to this Vagrantfile).
  #
  # The Opscode Platform uses HTTPS. Substitute your organization for
  # ORGNAME in the URL and validation key.
  #
  # If you have your own Chef Server, use the appropriate URL, which may be
  # HTTP instead of HTTPS depending on your configuration. Also change the
  # validation key to validation.pem.
  #
  # config.vm.provision :chef_client do |chef|
  #   chef.chef_server_url = "https://api.opscode.com/organizations/ORGNAME"
  #   chef.validation_key_path = "ORGNAME-validator.pem"
  # end
  #
  # If you're using the Opscode platform, your validator client is
  # ORGNAME-validator, replacing ORGNAME with your organization name.
  #
  # If you have your own Chef Server, the default validation client name is
  # chef-validator, unless you changed the configuration.
  #
  #   chef.validation_client_name = "ORGNAME-validator"
end
```

# Plugins

-  [vagrant-hostsupdater](https://github.com/cogitatio/vagrant-hostsupdater) : `$ vagrant plugin install vagrant-hostsupdater` to update your `/etc/hosts` file automatically each time you start/stop your vagrant box.

# Credits

[https://gist.github.com/wpscholar/a49594e2e2b918f4d0c4](https://gist.github.com/wpscholar/a49594e2e2b918f4d0c4)



---

> Bento [@quanblue](https://bento.me/quanblue) &nbsp;&middot;&nbsp;
> GitHub [@QuanBlue](https://github.com/QuanBlue) &nbsp;&middot;&nbsp; Gmail quannguyenthanh558@gmail.com
