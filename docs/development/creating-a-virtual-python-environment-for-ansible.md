## Creating an Ansible virtual python environment

First you will want to start a new terminal session.

### Using the latest version of Ansible

Again, in order the versions of Ansible that are available for installation you can use the `pip3 install ansible==` command with no version as we did when we created our mkdocs-material virtual environment.

As in the mkdocs-material virtual environment creation we prefix our command using sudo so that it will run with out generating a permissions error.

Again, we will examine the output in order to determine that the latest available version of Ansible that is installable using pip3: 

```shell
sudo pip3 install ansible==
```

In my case, the latest released version is 2.10.4

### Creating a Python 3 virtual environment for your Ansible installation

```shell
python3 -m venv ~/.venv/ansible-2.10.4
```

Next I activate the new Python environment. This will allow me to install Ansible into the new Python environment and will keep it sandboxed from my system level Python and any other virtual python environments that I create

```shell
source ~/.venv/ansible-2.10.4/bin/activate
```

Once activated your command prompt will be prefixed with name of the active virtual environment.

In my case my new command prompt looks like this:

```shell
(ansible-2.10.4) csteel@p1u20:~/MEGAsync/projects/ansible-project-expo$ 
```

Virtual environment confirmation

Next we confirm the location of current virtual environments pip3 command:

```shell
which pip3
```

Example output:

```shell
/home/csteel/.venv/ansible-2.10.4/bin/pip3
```

### Installing Ansible

Once we are in our virtual environment we install our targeted version of Ansible:

```shell
pip3 install ansible==2.10.4
```

#### Confirmation

We can confirm our installation using:

```shell
which ansible-galaxy
```

and perform a version check as well if desired:

```shell
ansible-galaxy --version
```

In my case the version information was incorrect! I installed version 3.10.4 but the version information showed 3.10.3 indicating that perhaps the developer(ers) failed to update the versioning file! 

Output example:

```shell
ansible-galaxy 2.10.3
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/csteel/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/csteel/.venv/ansible-2.10.4/lib/python3.8/site-packages/ansible
  executable location = /home/csteel/.venv/ansible-2.10.4/bin/ansible-galaxy
  python version = 3.8.5 (default, Jul 28 2020, 12:59:40) [GCC 9.3.0]
```

#### Creating an alias using bash_magic

```shell
nano ~/bin/bash_magic/bash_aliases.d/ansible-2.10.4.sh
```

entry example

```shell
alias ansible-2.10.4='source ~/.venv/ansible-2.10.4/bin/activate'
```

Make it executable

```shell
chmod +x ~/bin/bash_magic/bash_aliases.d/ansible-2.10.4.sh
```

create symlink to the bash magic shell script

```shell
cd ~/.bash_aliases.d/
ln -s ~/bin/bash_magic/bash_aliases.d/ansible-2.10.4.sh .
source ansible-2.10.4.sh
```

Return to previous directory

```shell
cd -
```

Test your new alias

```shell
ansible-2.10.4
```

your command prompt should change to reflect your pip3 installation. You may want to change to your mkdocs-material.someversion and then back to your ansible virtual environment to ensure that all if good. My command prompt looked like this:

```shell
(ansible-2.10.4) csteel@p1u20:~/MEGAsync/projects/ansible-project-expo$ 
```

