Event Notify Test Runner
========================

A utility for running arbitrary commands when files change. Uses [kqueue(2)] or
[inotify(7)] to avoid polling.  `entr` was written to make rapid feedback and
automated testing natural and completely ordinary.

Source Installation - BSD, Mac OS, and Linux
--------------------------------------------

    ./configure
    make test
    make install

To see available build options run `./configure -h`

Source Installation - Windows Subsystem for Linux
-------------------------------------------------

    wget http://eradman.com/entrproject/patches/entr-3.9-wsl
    patch -p1 < entr-3.9-wsl
    ./configure
    make install

The source patch is the current workaround for deformed [inotify
support on WSL](https://github.com/Microsoft/BashOnWindows/issues/2507).

Source Installation - Docker for Mac
------------------------------------

    wget http://eradman.com/entrproject/patches/entr-3.9-docker
    patch -p1 < entr-3.9-docker
    ./configure
    make install

The source patch is the current workaround for deformed [inotify
support on Docker for Mac](https://github.com/docker/for-mac/issues/896).

Man Page Examples
-----------------

Rebuild a project if source files change, limiting output to the first 20 lines:

    $ find src/ | entr sh -c 'make | head -n 20'

Launch and auto-reload a node.js server:

    $ ls *.js | entr -r node app.js

Launch and auto-reload a node.js server as a background task:

    $ (ls *.js | entr -r node app.js &)

Clear the screen and run a query after the SQL script is updated:

    $ echo my.sql | entr -p psql -f /_

Rebuild project if a source file is modified or added to the src/ directory:

    $ while true; do ls src/*.rb | entr -d make; done

News
----

A release history as well as features in the upcoming release are covered in the
[NEWS] file.

[kqueue(2)]: http://man.openbsd.org/kqueue.2
[inotify(7)]: http://man.he.net/?section=all&topic=inotify
[NEWS]: https://raw.githubusercontent.com/eradman/entr/master/NEWS
