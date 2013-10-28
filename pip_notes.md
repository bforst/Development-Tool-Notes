# Notes on pip usage

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

## Maintaining the Wheelhouse



Periodically, rec

* `pip-3.3 wheel pip setuptools wheel requests bpython ipython tornado pyzmq jinja2 sqlalchemy numpy matplotlib pandas ipython-sql`
* `pip-2.7 wheel pip setuptools wheel requests bpython ipython tornado pyzmq jinja2 sqlalchemy numpy matplotlib pandas ipython-sql`
