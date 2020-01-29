# Installing Python

This repo simply is a few notes on how to install Python on various operating
systems. As I teach Python classes regularly, I tend to get to know early if
something has changed over time, so hopefully I will be able to keep this guide
up to date.

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

Hint: Copy & paste the following commands into your Terminal window line by line.
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
pip install virtualenvwrapper
echo -e "export VIRTUAL_ENV_DISABLE_PROMPT=" >> ~/.bashrc
echo -e "export VIRTUALENVWRAPPER_PYTHON=$(which python)" >> ~/.bashrc
echo -e "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.bashrc
```

Close your Terminal, then re-open your Terminal and type `virtualenv --version`.
You should see something like `16.7.9`.

# Windows

Download the latest Python version from https://python.org/downloads

Execute the downloaded `*.exe` file. When the installation wizard appears, make sure to check the box "Add Python 3.X to PATH", then click at "Install Now".

At the end of the installation, click at the option "Disable path length limit", then close the wizard.

Now go to https://git-scm.com/download/win and download Git.


Execute the downloaded `*.exe` file. In the installation wizard, just click "Next" on every screen, no need to change anything.

In the Windows Startmenu search for "Git" and open "Git Bash".

Type `touch .bash_profile` then type `notepad .bash_profile` and paste the following line at the end of the file: `alias python='winpty python.exe'`, save the file in notepad and close notepad. Also close Git Bash.

Now search for Git again in the Startmenu and start it one more time.

Type `python` into the Git Bash terminal. If everything went well, you should see the Python prompt. Exit the Python prompt by typing `exit()`.

Now type the following things into your Git Bash terminal:

```
pip install pip --upgrade
pip install virtualenv
pip install virtualenvwrapper-win
```

After you have done this, you should close the Git Bash window, open a new one and type `mkvirtualenv.bat` and see if the mkvirtualenv program can be found. If you get some output, congratulations, you are done!

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

Alternatively, in VSCode, you can press `COMMAND + SHIFT + X` to get to the
Extensions manager and search for Python and then install the one named
`Python` (with 14+M downloads).

If you are on Windows, you should also do the following: In VSCode, click at "Terminal > New Terminal". A little window will show up at the bottom of the editor. You should see a drop down list where the active item is "1: powershell". CLick at this drop down list and select "Select Default Shell". Some options will show up at the top of the screen. Select "Git Bash".
