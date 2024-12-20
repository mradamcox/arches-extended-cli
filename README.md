# Arches Extensions

- [Overview](#overview)
- [Installation]
- [Command structure](#command-structure)

## Overview

The purpose of this package is unify some custom utilities that I've developed on and off while I work on different Arches projects. It is a work in progress. Hopefully, some of this content will eventually become part of core Arches, and in the meantime I hope others find it helpful.

So far, it is just a suite of Django management commands, though more content may be added in the future.

**repo** -- [legiongis/arches-extensions](https://github.com/legiongis/arches-extensions)

**docs site** -- [legiongis.github.io/arches-extensions](https://legiongis.github.io/arches-extensions).

**get in touch** -- Feel free to [open a ticket](https://github.com/legiongis/arches-extensions/issues) or get in touch directly, adam@legiongis.com. I'd love to collaborate if you see something here that could be better, or if you have ideas for other utilities that should be added. The only requirement is that the content be generic, not implementation-specific.

.. warning::
    These commands have been developed alongside Arches 6.x, and may not be compatible with Arches 7+.

## Installation

### For use in existing Arches project

These tools are packaged as a Django app so they can be easily integrated into an existing Arches installation. For this to work, you must install this package into your Arches virtual environment like this:

```
pip install git+https://github.com/legiongis/arches-extensions.git --no-binary arches-extensions
```

Now, in your Arches project's `settings.py` file, add `arches_extensions` to your `INSTALLED_APPS`:

```
INSTALLED_APPS += ('arches_extensions', )
```

It may be wiser to place this in your project's `settings_local.py` file, just remember to import `INSTALLED_APPS`:

```
from .settings import INSTALLED_APPS
INSTALLED_APPS += ('arches_extensions', )
```

That's it! You can now start using these management commands and other utilities in your existing Arches project.

To confirm the installation, run

```
python manage.py --help
```

and you should see a new section called `arches_extensions` with a list of new commands.

### For development/contribution

Because this is a Django app, it must be installed and developed within an Arches (Django) project, as the documentation generation needs to be run from within a Django context.

To create a development installation, you can fork/clone the repo and then pip install from that clone:

```
git clone https://github.com/legiongis/arches-extensions
pip install -e arches-extensions[dev]
```

Now add `arches_extensions` to your Arches `INSTALLED_APPS` as described above. Use `python manage.py --help` to confirm installation.

You can now edit within the local clone of the repo, and your changes will be reflected whenever you run a management command.

#### Build documentation

Documentation for this project is autogenerated from docstrings within the code using [pydoc](https://pdoc.dev/) and published with GitHub pages. From within your Arches project, run

```
python manage.py generate_arches_extensions_documentation
```

And you should see new HTML content added to the `/docs` directory within your local clone. Commit and push this content and GitHub pages will be rebuilt.

### Uninstall

To uninstall the app, remove `arches_extensions` from `INSTALLED_APPS` and then run

```
pip uninstall arches-extensions
```

## Command structure

The management commands herein are generally designed like:

    python manage.py [topic] [operation] [--extra-options]

Where the topic may be `maplayer` and an operation may be `list` (list all maplayers).

For help, use

```
python manage.py [command] --help
```

to learn more about any specific command.

A brief overview of each command is provided below, but for the real details you should head to `management/commands` and browse the submodules documentation.

.. warning:: 
    **These are all a work in progress, some will surely fail right now**
    
.. danger:: 
    Be aware that some of the commands will alter database content, though any changes to like this should be preceded with a confirmation prompt.
