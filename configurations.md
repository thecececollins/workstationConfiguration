## Configurations for your Mac environment
_Updated: August 11, 2018_

This works with macOS High Sierra (10.13), Sierra (10.12), OS X El Capitan (10.11), OS X Yosemite (10.10), or Mavericks (10.9) and uses Homebrew as a package manager. I streamlined this tutorial in August 2014 to make it even easier to set up your development environment. I’ve archived the original version. In January 2016, I added support for xip.io, which is a DNS redirecting service. This allows you to access your local sites from any device on your network.

### Terminal Configurations
- Vim: https://www.engadget.com/2012/07/10/vim-how-to/

### Terminal Tools
- PuTTy: https://www.ssh.com/ssh/putty/mac/

### Setting Up Homebrew
Homebrew provides a package management system for macOS, enabling you to quickly install and update the tools and libraries that you need. Follow the instructions on the site.

- You should also amend your PATH, so that the versions of tools that are installed with Homebrew take precedence over others. To do this, edit the file _~/.bashprofile in your home directory to include this line:

`export PATH="/usr/local/bin:/usr/local/sbin:~/bin:$PATH"`

_You need to close all terminal windows for this change to take effect._

- To check that Homebrew is installed correctly, run this command in a terminal window:

`brew doctor`

- To update the index of available packages, run this command in a terminal window:

`brew update`


### Installing the Git Version Control System
The Xcode Command Line Tools include a copy of Git, which is now the standard for Open Source development, but this will be out of date.

- To install a newer version of Git than Apple provide, use Homebrew. Enter this command in a terminal window:

`brew install git`

_If you do not use Homebrew, go to the Web site and follow the link for Other Download Options to obtain a macOS disk image. Open your downloaded copy of the disk image and run the enclosed installer in the usual way, then dismount the disk image._

- Always set your details before you create or clone repositories on a new system. This requires two commands in a terminal window:

`git config --global user.name "Your Name"'
'git config --global user.email "you@your-domain.com"`

The global option means that the setting will apply to every repository that you work with in the current user account.

- To enable colors in the output, which can be very helpful, enter this command:

`git config --global color.ui auto`


### Choosing a Text Editor
Current versions of macOS include command-line versions of both Emacs and vim, as well as TextEdit, a desktop text editor. TextEdit is designed for light-weight word processing, and has no support for programming. Unless you already have a preferred editor, I suggest that you install either Atom or Visual Studio Code, which are powerful graphical text editors.

Whichever text editor you choose, remember to set the EDITOR environment variable in your _~/.bashprofile file, so that this editor is automatically invoked by command-line tools like your version control system. For example, put this line in your profile to make vim the favored text editor:

`export EDITOR="vim"`


### Setting Up Atom
To install Atom, enter this command in a terminal window:

`brew cask install atom`

- To make Atom your default editor, use this line in your _~/.bashprofile file:

`export EDITOR="atom -w"`

- You are expected to install extensions to customize the user interface. For example, these extensions provide some valuable enhancements to the user interface of Atom:

`apm install color-picker file-icons minimap`

- The file-icons package requires no configuration. Refer to the pages for color-picker and minimap for details on how to use them.

- Install code linters for the languages that you use. Atom automatically runs the appropriate linter for the files that you are editing.

- This command installs support into Atom for CSSLint, ESLint and yaml-js:

`apm install linter-csslint linter-eslint linter-js-yaml`
