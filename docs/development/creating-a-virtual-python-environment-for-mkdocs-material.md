# Creating a virtual python environment for mkdocs-material.md

## Requirements

* Python 3 (For older systems running Python 2 systems see Pyton 2 virtualenvs command.)
  * pip3
    * `sudo apt install python3-pip` on Ubuntu 20.04
  * venv
    * The [`venv`](https://docs.python.org/3/library/venv.html#module-venv) Python 3 module provides support for creating lightweight “virtual environments” with their >
    * [venv — Creation of virtual environments](https://docs.python.org/3/library/venv.html)
  * mkdocs-material
    * mkdocs-minify-plugin

## References

* [www.mkdocs.org](https://www.mkdocs.org/)
* [mkdocs-material/getting-started](https://squidfunk.github.io/mkdocs-material/getting-started/#adding-a-web-app-manifest)
* [mkdocs-material/contributing](https://squidfunk.github.io/mkdocs-material/contributing/)
* [squidfunk.github.io/mkdocs-material/](https://squidfunk.github.io/mkdocs-material/)
* [cjsteel/mkdocs-material](https://github.com/cjsteel/mkdocs-material/tree/master/docs)

## Virtual environment creation for mkdocs-material

Virtual environments allow you to run multiple Python applications as well as multiple versions of Python without making changes to the system Python.

In this example we will name our virtual Python environment for the application and version so that you can run multiple isolated application version.

### Determine the latest available version of `mkdocs-material`

We will use the outout of the command `pip3 install mkdocs-material==` in order to determine the latest stable version of mkdocs-material that is available for installation via pip3.

```shell
sudo pip3 install mkdocs-material==
```

In my case the latest version is 6.1.7.

### Creating your virtual environment

Before installing `mkdocs-material-6.1.7` I will to create and activate a Python virtual environment which will "sandbox" my install and prevent it from interfering with my systems version of Python and any system wide Python applications that I have.

```shell
python3 -m venv ~/.venv/mkdocs-material-6.1.7
```

### Activating your mkdocs-material virtual environment

```shell
source ~/.venv/mkdocs-material-6.1.7/bin/activate
```

Once the environment is activated your command prompt will become prefixed with the name of the active virtual (Python) environment. Mine looks like this:

```shell
(mkdocs-material-6.1.7) csteel@p1u20:~/MEGAsync/projects/ansible-project-expo$ 
```

### Test and confirmation

Before continuing we will take a moment to ensure that everything is working as it should be.
With your new environment is activated the location of your default version of pip3 will change to the virtual environments. We can confirm this by running:

```shell
which pip3
```

The output should reflect the directory that your virtual environment is created in. For this example that would be something similar this this:

```shell
/home/csteel/.venv/mkdocs-material-6.1.7/bin/pip3
```

### Install mkdocs-material

Now that your virtual environment is active, any pip3 installs will be installed to the virtual environment insulating it from any other virtual environments you might have as well as any pip3 installs that have been made using your systems pip3 version.


```shell
pip3 install mkdocs-material==6.1.7
```

By the way, you may have some red output error output. Don't panic just yet. You might want to make a note of the error.
In my case everything worked well in spite of the error. You might also want to try reinstalling, but again, an error does not neccesarily mean that things have failed

### install any required plugins

When this document was last edited the expo project was using the mkdocs-minify-plugin plugin.

Ensure that your mkdocs-material virtual environment is active and install the plugin:

```shell
pip3 install mkdocs-minify-plugin
```

During my installation I got an error:

```shell
  ERROR: Failed building wheel for jsmin
```

Running the command again gave no error.

### Serve the projects documentation

Now that all of the requirements have been installed you should be able to run the built in mkdocs server in order to view the expo projects documentation in your development systems' browser.

The expo projects root directory contains a file called `mkdocs.yml`. Change to your expo projects root directory and then run the `mkdocs serve` command:

```shell
mkdocs serve
```

You will see some output which includes a message similar to this:

```shell
[I 201208 06:59:18 server:335] Serving on http://127.0.0.1:8000
```

By default your documentation will be available at the URL mentioned above. You can copy and paste this to your local browser and view this documentation in your browser if your **firewall** is not blocking port 8000 or some other issue has occured.

## Creating an alias using bash_magic

### Create your source alias script

Add a script and open it for editing in your bash_magic bin aliases directories.
```shell
nano ~/bin/bash_magic/bash_aliases.d/mkdocs-material-6.1.7.sh
```

Example entry:

```shell
alias mkdocs-material-6.1.7='source ~/.venv/mkdocs-material-6.1.7/bin/activate'
```

Make it executable

```shell
chmod +x ~/bin/bash_magic/bash_aliases.d/mkdocs-material-6.1.7.sh
```

Create your symlink

```shell
cd ~/.bash_aliases.d/
chmod +x ~/bin/bash_magic/bash_aliases.d/mkdocs-material-6.1.7.sh
ln -s ~/bin/bash_magic/bash_aliases.d/mkdocs-material-6.1.7.sh .
```

Source your symlink

```shell
source mkdocs-material-6.1.7.sh
```

Return to your previous directory location

```shell
cd -
```

# test your new alias

```shell
mkdocs-material-6.1.7.sh
```

