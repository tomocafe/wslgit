# wslgit

Wrapper to seamlessly use the Windows native `git.exe` in WSL when you are in the Windows filesystem, otherwise use WSL native `git`.

Using the WSL `git` on a repository located in the Windows filesystem results in slow performance. When you can't move that repository into the WSL filesystem but you prefer to work in the WSL environment, this script can help.

## Usage

1. Add the `wslgit` script to your `PATH` (optional, but recommended)
2. Create an alias

   ```bash
   git () { wslgit "$@"; }
   export -f git
   ```

Most likely it will *just work*, but there are some environment variables you can set to tune `wslgit` to your specific needs:

* `WSLGIT_EXE`: your Windows git executable (defaults to `git.exe`)
* `WSLGIT_ONLY`: string containing space separated git commands. `wslgit` will only switch to Windows git when using these subcommands.
* `WSLGIT_IGNORE`: string containing space separated git commands. `wslgit` will switch to Windows git for all subcommands *except* these.
* `WSLGIT_QUIET`: don't print the hint that `wslgit` switched over to Windows git. (Note: this will never be printed unless you are attached to a terminal.)
* `WSLGIT_DEBUG`: prints the final command
* `WSLPWD`: the working directory when invoked (defaults to `.`)

## Details

This wrapper works with:

* custom subcommands defined in WSL
* git commands with POSIX paths in arguments
