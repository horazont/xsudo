# `xsudo`

## Name

`xsudo` – Execute an X11 application as a different user with the current user’s X11 server

## Synopsis

```console
$ xsudo [-u USER] [-i] [-h] [--] COMMAND [ARGS...]
```

## Description

This script executes the given `COMMAND` (with the following `ARGS`) as
the given `USER`, using the X11 server of the invoking user.

In contrast to `ssh` with `-X`, this avoids having to pass all
communication with the X11 server through a socket, which is generally
much slower (and makes some applications fail).

**Note:** Do not run graphical applications as root. They generally have
a way too large attack surface, and I’m also pretty sure that
applications share the same X11 server can do nasty things to each
other.

**Note:** In the same vein, do not rely on this as a security tool. You
may want to look into Mandatory Access Control, such as SELinux or
AppArmor.

**Note:** The target user must be able to read and execute the `xsudo`
command.

When executing the command, it is run using a login-shell mode `bash`
shell. This can currently not be turned off or changed.

## Options

* `-u`: The name of the user to run the command as. This is
  required. *Do not pass `root` to this.*

* `-h` (`--help`): Print a short usage summary and exit.

* `-i`: Thoroughly clean the environment of the executed command. Only
  the XAUTHORITY and DISPLAY variables, along with anything set by the
  login shell will be present.

## Exit Status

`xsudo` exits with the exit status of the called command or 255 in case
of an internal error.

## Limitations and Known Bugs

- The command will always be executed under a `bash` login shell, even
  if the user has a different shell set. This should be fixed in a
  future version.

- `xsudo` always changes directory to the home directory of the target
  user. This is intended as a convenience function.

## Bug Reports

Report any bugs or issues you encounter to the
[Bugtracker on GitHub](https://github.com/horazont/xsudo/issues).

## See Also

ssh(1) with the `-X` option, kdesudo(1), gksudo(1)

## Authors

Jonas Schäfer, inspired by
[an answer to my question on SuperUser](https://superuser.com/a/1527506/122572)
on how to substitute kdesudo and gksudo.
