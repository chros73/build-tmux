.. contents:: **Contents**

build-tmux
============

Builds optimized version of `tmux <https://github.com/tmux/tmux>`_ including patches into custom location on Debian flavoured systems.

Supports:

- multiple release versions
- latest release version
- git version (by specifying branch or commit)
- building per user then "installing" system wide

Limitations:

- no static build


Compilation
-----------

Installing build dependencies
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First, you need to install a few **required** packages — **and no, this is not optional in any way**. They require about ``230 MB`` disk space. These steps must be performed by the ``root`` user (i.e. in a root shell, or by writing ``sudo`` before the actual command):

.. code-block:: shell

   apt-get update
   apt-get install sudo coreutils binutils build-essential git time \
       curl locales autoconf automake pkg-config \
       libevent-2.0-5 libtinfo5 libutempter0 \
       libevent-dev libncurses5-dev libutempter-dev


Getting repo
^^^^^^^^^^^^

.. code-block:: shell

   mkdir -p ~/src/; cd ~/src/
   git clone https://github.com/chros73/build-tmux.git
   cd build-tmux


Compiling for regular user
^^^^^^^^^^^^^^^^^^^^^^^^^^

It has to be compiled this way first. Build script creates local CPU optimized code by default.

It will build ``tmux`` binary into ``~/lib/tmux*`` directory and create symlinks to it, e.g. in ``~/bin/`` directory.

.. code-block:: shell

   time nice -n 19 ./build.sh tmux

You can compile the ``latest`` release version or the specified ``git`` version by adding a ``latest`` or ``git`` second argument to the above commands.

If you want to turn off optimization for some reason (e.g. debugging or moving the build to a different box) it can be done by adding ``optimize_build=no`` in front of the above command, e.g.:

.. code-block:: shell

   optimize_build=no time nice -n 19 ./build.sh tmux git


Install it into system
^^^^^^^^^^^^^^^^^^^^^^

It installs (copies) the compiled ``tmux`` binary into ``/opt/tmux*`` directory and creates symlinks to it, e.g. in ``/usr/local/bin/`` directory. Needs root shell, or by writing ``sudo`` before the actual command:

.. code-block:: shell

   ./build.sh install

If you specified a second argument (``latest`` or ``git``) during compilation then you have to use the same here as well.


Change log
----------

See `CHANGELOG.md <CHANGELOG.md>`_ for more details.
