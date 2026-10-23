# WSL Hosts

On some WSL installations DNS is not forwarded to the Linux kernel, so lerd's DNS never sees the lookups and its domains only resolve through the hosts files. This plugin writes a `127.0.0.1 <domain> # lerd` line for every site domain (including worktree domains) and every service domain into both the Windows hosts file and `/etc/hosts`.

Lines ending in `# lerd` are rewritten on every sync. Every other line is left alone, and a domain you already map to `127.0.0.1` by hand gets no extra line.

## Command

`lerd wsl-hosts:sync` syncs both files: the Windows file through a UAC prompt, `/etc/hosts` through `sudo`. It then lists every domain and where each file maps it (`lerd`, `own line` or `MISSING`).

`lerd wsl-hosts:sync -n` shows the diff for both files and changes nothing.

Run the sync after `lerd link`, a new worktree or `lerd service domain`.

## Settings

None.
