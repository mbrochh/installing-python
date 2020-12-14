# Installing Python

This repo contains just a few notes on how to install Python on various operating
systems. As I teach Python classes regularly, I tend to get to see all the quirks
and pitfalls during Python installations, so hopefully I will be able to keep this 
guide up to date.

To get your machine up and running, please follow the instructions for your operating 
system (either MacOS or Windows 10) AND the instructions for VSCode at the very bottom.

## MacOS

Hint: You can open a Terminal window by pressing `COMMAND + SPACE` and then
typing `Terminal`.

Before you can do proper software development on your Mac, you must download
XCode from the AppStore (this will take very long). Once installed, just open
XCode and accept the license agreement, then close it again. Then open a
Terminal window and type `xcode-select --install`

Python is already installed on your Mac, but chances are that you have a very
old version. In your Terminal app, type `python --version` and you should see
something like `Python 2.7.3`.

These days, you should work with `Python 3+`, so let's install it:

First, install Homebrew. You can find out more here: https://brew.sh/

Execute the following command in your Terminal:

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Now install Python via the following commands. Note: We assume that you are
using the standard Terminal with bash. If you use some other Terminal or some
other shell, you might have to replace `~/.bashrc` in the code below with
something else like `~/.zshrc` if you use ZSH, for example).

IMPORTANT: Always copy & paste code snippets into your Terminal window line by line.
Do not copy & paste the entire script at once.

```
brew update
brew install pyenv
pyenv install 3.8.1
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc
source ~/.bashrc
pyenv global 3.8.1
pip install pip --upgrade
python --version
```

The last command should print the correct Python version: `Python 3.8.1`.

**Bonus**:

This is not necessary for most beginner classes, but eventually you will want
to install `virtualenvwrapper`. You can install it like so:

```
brew install pyenv-virtualenvwrapper
echo -e 'export PYENV_VIRTUALENVWRAPPER_PREFER_PYVENV="true"' >> ~/.bashrc
echo -e "export WORKON_HOME=$HOME/.virtualenvs" >> ~/.bashrc
echo -e "pyenv virtualenvwrapper_lazy" >> ~/.bashrc
```

Close your Terminal, then re-open your Terminal and type `which workon`.
You should see something like this:

```
workon () {
	virtualenvwrapper_load
	workon "$@"
}
```

# Windows 10

If you have a computer that does not run Windows 10, but an older version, please 
try to upgrade your computer to Windows 10. 

Windows 10 has something called "Windows Subsystem for Linux" (WSL), which allows
us to run Ubuntu inside Windows seamlessly. It is really quite amazing.

Most of my instructions here were stolen from this post: https://pbpython.com/wsl-python.html

Click at the Windows Search in your Start Menu and search for "Powershell", then right-click it
and chose "Run as administrator".

IMPORTANT: Always copy & paste code snippets into your Terminal window line by line.
Do not copy & paste the entire script at once.

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Now restart your computer.

Next search for the "Microsoft Store". Then search for "Ubuntu". Select "Ubuntu 20.04 LTS" 
and click at "Get". It is a 444MB download and should take around 5-10 minutes.

Once it is downloaded, click at "Launch". A Terminal window will appear and you will have
to choose your Ubuntu username and password. It is best to use the same username and 
password that you also use for your Windows account. Once you have set your password,
you can close the window. Next, we will install a better Terminal for you.

Open the "Microsoft Store" again and search for "Windows Terminal". Click at "Get" again
and once installed, click at "Launch". When the Terminal launches, type `wsl`. You 
should remember this, this is how you get into Ubuntu: You launch "Windows Terminal" and
then you type `wsl`.

Now that you are logged into Ubuntu, let's install quite a lot of software:

IMPORTANT: Always copy & paste code snippets into your Terminal window line by line.
Do not copy & paste the entire script at once. 

You don't need to copy & paste the lines that start with a `#`, those are just 
comments for your better understanding.

```
sudo apt update
sudo apt upgrade
# the above will take 5-10 minutes

sudo apt-get install python3-pip git gcc make openssl libssl-dev libbz2-dev libreadline-dev libsqlite3-dev
# the above will take 5-10 minutes

curl https://pyenv.run | bash
# the above will take 2-6 minutes

sudo apt-get install virtualenv virtualenvwrapper
# the above should be quite fast

cp ~/.bashrc ~/.bashrc.backup
mkdir ~/virtualenvs
echo -e "export WORKON_HOME=$HOME/virtualenvs" >> ~/.bashrc
echo -e "VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3" >> ~/.bashrc
echo -e ". /usr/share/virtualenvwrapper/virtualenvwrapper.sh" >> ~/.bashrc
# for the next command, replace `{USERNAME}` (incl the braces) with your username
# for example, if your username is bob, then the command should be
# echo -e 'export PATH="/home/bob/.pyenv/bin:$PATH"' >> ~/.bashrc
echo -e 'export PATH="/home/{USERNAME}/.pyenv/bin:$PATH"' >> ~/.bashrc
echo -e 'eval "$(pyenv init -)"' >> ~/.bashrc
echo -e 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
source ~/.bashrc
```

At this point, everything should be installed. To verify, you can
try the following things:

Type `python3 --version` - you should see the Python version.

Type `pip3 --version` - you should see the Python version.

Type `mkvirtualenv` - you should see some help text about this command.

Type `pyenv` - you should see some help text about this command.

# VSCode

In my classes, you will need a text editor to write your code. The best free
text editor to write code these days is VSCode. Please download and install it
from here: https://code.visualstudio.com/download

If you are on Windows: when you start the installation wizard, make sure to activate all checkboxes under "Other" on the "Select Additional Tasks" page.

If you are on MacOS: Once installed, open VSCode. Now press `COMMAND + SHIFT + P` and type `PATH`.
You should see an option called `Shell Command: Install 'code' command in PATH`.
Select that option.

Now you should be able to close all Terminal windows, then re-open a new
Terminal window and type `code` and it should start VSCode.

Finally, you should install the Python extension. You can visit this URL and
click at the `Install` button: https://marketplace.visualstudio.com/items?itemName=ms-python.python

If you are on Windows, you should also install the WSL extension. You can visit
this URL and click at the `Install` button: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack

After all this is done, close all terminals and all VSCode windows, then open the `Windows Terminal` and type `code`. As a result, VSCode should open up.

# Jupyter Notebook

In order to install the Jupyter Notebook on your local machine, you must follow all the steps above, then you can try the following:

Open the `Windows Terminal`.

Type `pip3 install jupyter`. The installation will take a while.

Type `jupyter notebook`. You will see a red error message, but that is OK. Right above the error message, you will find two URLs. Copy the one with `localhost:8888` and paste it into Google Chrome. NOTE: Jupyter has now "taken over" the control over your terminal and is running a web-server. You cannot enter any commands into this terminal window any more. If you want to do anything in a terminal, you must open a new terminal window, while Jupyter keeps running in this terminal window. If you ever want to stop Jupyter, you can press `CTRL+C` in the terminal window, and then confirm with `y`.

You will now see the Jupyter Notebook. 

You might want to click at `New` and then `Folder`. This will create a folder called `Untitled Folder` in your home directory. You can then click the checkbox next to that folder and select `Rename` at the top-left. You should name it `Notebooks`. Now click into that folder.

Finally, at the top right, click at "New" and select "Python 3". You can now start working on a notebook. The notebook will be saved inside whatever folder you clicked at, so in our case it should be inside the `Notebooks` folder. In the future, you can open that notebook again.
