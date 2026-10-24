# WSL Hosts

On some WSL installations DNS is not forwarded to the Linux kernel, so lerd's DNS never sees the lookups and its domains only resolve through the hosts files. This plugin writes a `127.0.0.1 <domain> # lerd` line for every site domain (including worktree domains) and every service domain into both the Windows hosts file and `/etc/hosts`.

Lines ending in `# lerd` are rewritten on every sync. Every other line is left alone, and a domain you already map to `127.0.0.1` by hand gets no extra line.

## Command

`lerd wsl-hosts:sync` syncs both files: the Windows file through a UAC prompt, `/etc/hosts` through `sudo`. It then lists every domain and where each file maps it (`lerd`, `own line` or `MISSING`).

`lerd wsl-hosts:sync -n` shows the diff for both files and changes nothing.

## Notifications

Linking a site, adding a worktree and starting a service check both hosts files without changing them. When a domain is missing from either, lerd shows a **wsl-hosts: Hosts files out of date** notification naming the domains, and you run `lerd wsl-hosts:sync`. A newer one replaces the last, so they do not pile up. lerd asks whether to allow them when the plugin is installed; change your answer on the plugin's card, under **Plugin messages** in lerd's notification settings, or with `lerd plugin notifications wsl-hosts on|off`. Until they are allowed, the message goes to `hooks.log` in the plugin's data folder instead.

Changing a service's domain with `lerd service domain` fires no event, so run the sync yourself after it.

## Settings

None.
