# Notes on pip usage

## Sources

The following documentation has been useful in understanding pip:

* [pip Project Documentation](http://pip-installer.org)
* [pip Usage](http://www.pip-installer.org/en/latest/usage.html)
* [pip Cookbook](http://www.pip-installer.org/en/latest/cookbook.html)
* [pip Configuration](http://www.pip-installer.org/en/latest/configuration.html)

## Environment Variables

The command line options for pip can be set with environment variables using the format:

* `PIP_<UPPER_LONG_NAME>`
* Dashes (-) have to replaced with underscores (_).

The following environment variables have been set specifically for pip. They will affect the behaviour of all instances of pip.

* `PIP_USE_WHEEL=true`
    * Affects the following commands:
        * install: will preferentially install from wheel archives.
        * wheel: unsure how this will affect the command.
        * bundle: unsure how this will affect the command.
* `PIP_WHEEL_DIR=$HOME/.wheelhouse`
    * Affects the following command:
        * wheel: builds wheels in this directory.
* `PIP_FIND_LINKS="$PIP_WHEEL_DIR"`
    * For finding targets, uses the directory where wheels are stored.
    * Affects the following commands:
        * install: will use files in this directory for installation if possible.
        * freeze: will include a -f option with this directory in the freeze output.
        * list: unsure how this will affect the command.
        * wheel: unsure how this will affect the command.
        * bundle: unsure how this will affect the command.

Instead of environment variables, plain old .ini configuration files located at `$HOME/.pip/pip.conf` can be used. This allows for finer-grained application of certain switches. For example, the following config will only use the urls in the install section for the install command, but will use the link in the global section for all other commands.

    [global]
    find-links =
        http://download.example.com
    
    [install]
    find-links =
        http://mirror1.example.com
        http://mirror2.example.com

## Maintaining the Wheelhouse

The Wheelhouse is where you store the wheel files to give you fast local installs. This has been set by the `PIP_WHEEL_DIR` environment variable above. Paired with the `PIP_FIND_LINKS` variable, the given directory will automatically be used for creating new wheels without requiring the `--find-links` option.

Periodically, you will want to delete the contents of the Wheelhouse and recreate all of the wheels that were in there. There is a monthly task in your calendar to perform this action. This should also happen after any major OS upgrade. After running this task, you should also activate all of your virtual environments, run `pip list -o`, and upgrade any libraries that have fallen out of date (whose exact version you don't care about).

As the list of libraries that you needs grows, add them to the list following the `wheel` command.

* After running the first command, the second command may fail noting that files/folders already exist and it does not want to over-write them. Open the temp folder that it complains about, delete all of the contents, and re-run if this occurs.
* `pip-3.3 wheel pip setuptools wheel requests bpython flask django pytest ipython tornado pyzmq jinja2 sqlalchemy numpy matplotlib pandas ipython-sql`
* `pip-2.7 wheel pip setuptools wheel requests bpython flask django pytest ipython tornado pyzmq jinja2 sqlalchemy numpy matplotlib pandas ipython-sql`

## Command-line Auto-completion

To turn on tab-completion of pip commands and options, add the following to your .profile after modifying your path so that pip can be found: ``eval "`pip completion --bash`"``

## Freezing Requirements

