Package Setup
=============

No installation is required to run the *lnifmri_prep* workflow: just copy/clone the repository to any location in the filesystem and make the scripts executable::

	user@host:~$ git clone https://github.com/tambalostefano/lnifmri_prep.git
	user@host:~$ cp path/to/lnifmri_prep path/to/my/lnifmri_prep
	user@host:~$ chmod a+x path/to/my/lnifmri_prep/lnifmri_prep* 

Then add an environment variable ($LNIFMRIDIR) to your *$PATH* in .profile or .bash_profile::

	user@host:~$ nano .profile

Locate the definition of the *$PATH* variable and add *path/to/my/lnifmri_prep*::

	LNIFMRIDIR=path/to/my/lnifmri_prep
	PATH=$LNIFMRIDIR:$PATH
	export LNIFMRIDIR PATH

Save the updated file and source it::

	user@host:~$ source .profile

The changes will be effective in the current terminal session.

.. note::
	To make the changes persistent, you must log out and log back in.

Additional steps for macOS users
--------------------------------

Most of the command-line tools used in *lnifmri_prep* are available also on MacOS (>10.5) with some limitations. These are mainly due to slightly different implementation of the BSD-based UNIX tools that run under MacOS. The simplest way to overcome these limitations is to install GNU-based core utilities along with builtin BSD tools. You will need `Homebrew <https://brew.sh>`_ and `coreutils <https://formulae.brew.sh/formula/coreutils#default>`_

Install Homebrew::

	MacUser@host:~$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

Install GNU-coreutils::

	MacUser@host:~$ brew install coreutils

And pay attention to the very last message after the installation::

	Commands also provided by macOS have been installed with the prefix "g".
	If you need to use these commands with their normal names, you
	can add a "gnubin" directory to your PATH from your bashrc like:
    PATH="$(brew --prefix)/opt/coreutils/libexec/gnubin:$PATH"

