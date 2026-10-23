# WSL Hosts

A [lerd](https://lerd.sh) plugin for lerd under WSL. On some WSL installations DNS is not forwarded to the Linux kernel, so lerd's domains only resolve through the hosts files. This plugin keeps the Windows hosts file and `/etc/hosts` in sync with lerd's site and service domains.

## Install

```sh
lerd plugin install https://github.com/ExeQue/lerd-plugin-wsl-hosts.git
```

Then run `lerd wsl-hosts:sync`. See [DOCS.md](DOCS.md).

## What it adds, reads and changes

- **Adds** the CLI command `lerd wsl-hosts:sync`.
- **Reads** `~/.local/share/lerd/sites.yaml` and `~/.config/lerd/config.yaml` for the domains, and both hosts files.
- **Changes** `C:\Windows\System32\drivers\etc\hosts` (through a UAC prompt) and `/etc/hosts` (through `sudo`), only lines ending in `# lerd`, and only when you run `lerd wsl-hosts:sync`.
- **Sends** nothing over the network.

## Requirements

WSL with Windows interop (`powershell.exe`, `cmd.exe`), `wslpath`, `iconv`.

## License

MIT, see [LICENSE](LICENSE).
