# `xsudo`

```
$ xsudo --help
usage: /usr/local/bin/xsudo [-u USER] [-i] [-h] [--] COMMAND [ARGS...]

Run an X11 application as a different user.

Optional arguments:

        -u USER The user to run the command as. Required.
        -i      Clean the environment
        -h      Print this help message

```

**Note:** This is **not** meant to be used to execute commands as root, which is why the ``-u`` option is required!

**Note:** The user passed to `-u` needs to be able to read and execute the script.
