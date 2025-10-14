# safer - run a command isolated to the current directory

# Nevermind, here's a much better idea: https://justine.lol/pledge/

Many dev tools are explicitly running arbitrary code directly from the internet with unknown chain of custody.
Most devs know we should probably have a separate user for to run these dev tools as, or use devcontainers or VMs but
often the convenience isn't good enough to actually do so.


## Usage
Should we have another tool in the toolbox that ofters some extra guard rails?
Something like:

```bash
$ cd foo-project
$ safer pip install foo
$ safer cargo run
$ safer npm install foo

# etc
```

Ideally this should work on linux, bsd, macos and maybe even windows.
For convenience the "safer" command should have read/execute access to the directories on the real users's $PATH
but only have read/write to the directory tree under the current working directory.

## What could the guard rails be?

* A temporary unix account with limited permissions?
* A temporary container created with systemd-nspawn or docker or freebsd jails?
* A temporary vm created with firecracker, qemu, whatever?
* Anything else?

## devcontainers etc

Devcontainers already probably hits this use case but the convenience isn't quite there to just casually fire off a single command in an arbitrary directory.
