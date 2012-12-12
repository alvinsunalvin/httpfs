httpfs - Remote FUSE filesystem via server-side script
======================================================

httpfs is a FUSE-based filesystem that uses HTTP messages to mount a remote
directory on a local machine, relying on a generated server-side script
(e.g. PHP) installed on the server.

Setup
-----

 1. Add the current user to the `fuse` group as described in the **Prepare the
    environment** paragraph.

 2. Install the dependencies. For Debian based distros just run:

        sudo apt-get install fuse libfuse-dev libcurl4-openssl-dev cmake

 3. Install:

        make
        sudo make install

 4. If needed, uninstall:

        sudo make uninstall

Sample usage
------------

 1. Generate a PHP script:

        httpfs generate php > httpfs.php

 2. Place the generated script in an accessible location inside the document
    root of your web server.

 3. Mount the remote filesystem:

        mkdir /tmp/httpfs/
        httpfs mount http://target.com/httpfs.php /tmp/httpfs/ /home/john/

 4. Now the remote `/home/john/` is mounted in `/tmp/httpfs/`, head there to
    browse the remote files.

 5. Unmount the filesystem:

        fusermount -u /tmp/httpfs/

Prepare the environment
-----------------------

Make sure the current user is in the `fuse` group, this preliminary step is
mandatory to use any FUSE filesystem. You can list the groups you belong to with
`groups`, if that includes `fuse` you're done, otherwise:

    sudo adduser john fuse

Then log out and back in or start a new shell with:

    newgrp fuse

to inform the system about the changes.

Resources
---------

FUSE - http://fuse.sourceforge.net

Authors
-------

Andrea Cardaci - http://cyrus-and.github.com

Emilio Pinna - http://disse.cting.org
