# WSL Hosts

A [lerd](https://lerd.sh) plugin for lerd under WSL. On some WSL installations DNS is not forwarded to the Linux kernel, so lerd's domains only resolve through the hosts files. This plugin keeps the Windows hosts file and `/etc/hosts` in sync with lerd's site and service domains, and tells you when they fall behind.

## Install

```sh
lerd plugin install https://github.com/ExeQue/lerd-plugin-wsl-hosts.git
```

Then run `lerd wsl-hosts:sync`. See [DOCS.md](DOCS.md).

## What it adds, reads and changes

- **Adds** the CLI command `lerd wsl-hosts:sync`, and hooks on `site.linked`, `worktree.added` and `service.started` that only check the hosts files.
- **Reads** lerd's own API with the token lerd gives the plugin, `/api/sites` and `/api/services`, for every site, worktree and service domain, and both hosts files.
- **Changes** `C:\Windows\System32\drivers\etc\hosts` (through a UAC prompt) and `/etc/hosts` (through `sudo`), only lines ending in `# lerd`, and only when you run `lerd wsl-hosts:sync`. The hooks change nothing.
- **Sends** a notification through lerd's own API (`POST /api/notifications/plugin`) when a domain is missing, once you allow the plugin's notifications (`notifications: true`; lerd asks at install). Nothing leaves the machine.

## Requirements

lerd 1.38 or newer, `python3`, `iconv`, `curl`, and WSL with Windows interop (`wslpath`, `powershell.exe`, `cmd.exe`). Until you allow the plugin's notifications, the hooks write the message to `hooks.log` instead.

## License

MIT, see [LICENSE](LICENSE).
