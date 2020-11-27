# venv

The [`venv`](https://docs.python.org/3/library/venv.html#module-venv) Python 3 module provides support for creating lightweight “virtual environments” with their own site directories 

## Resources

* [venv — Creation of virtual environments](https://docs.python.org/3/library/venv.html)

## Requirements

* Python 3 (For older systems running Python 2 systems see Pyton 2 virtualenvs command.)
* pip3
## Creating a Virtual Environment

Ubuntu 20.04 example:

```shell
# Determine lastest available version of Ansible
pip3 install ansible==
# Create Python 3 virtual environment:
python3 -m venv ~/.venv/ansible-2.10.3
# activate our new python 3 virtual environment:
source ~/.venv/ansible-2.10.3/bin/activate
# Once you have activated the new virtual environment your
# command prompt will be prefixed with the environments 
# name. In this example the new command prompt should
# look something like this:
#
#    (ansible-2.10.3) csteel@p1u20:~/home/csteel
which pip3 # Here we confirm the location of the pip3 default pip3 exectuable, it should be in our new virtual environment.
#
# Next we install the desired ansible version using pip3:
pip3 install ansible==2.10.3
```



