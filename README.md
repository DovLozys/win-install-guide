# win-install-guide

some notes on how I do it these days...

## Bootable USB

- Download windows .iso from <https://www.microsoft.com/software-download/windows11>
  - Product Language: en-us
  - verify .iso with `Get-FileHash` in PowerShell

- rufus win experience settings:
![Rufus settings](https://github.com/DovLozys/win-install-guide/assets/755086/7b13c307-7127-4329-b55b-aae4448c97f9)

## win installation

TODO: CTT install video summary

## Dev env

### VSCode

- `@tag:telemetry` set to off
- `Enables commit signing with GPG`

### wsl/git

- `wsl --install`
- .gitconfig:

```bash
git config --global user.email "dov@example.com"
git config --global user.name "Dov"
git config --global user.signingkey 00EF4D3F22885E4B
git config --global commit.gpgsign true
git config --global tag.gpgsign true
```

- install <https://www.gpg4win.org>
- in wsl edit `~/.gnupg/gpg-agent.conf` with:

```text
default-cache-ttl 34560000
max-cache-ttl 34560000
pinentry-program "/mnt/c/Program Files (x86)/GnuPG/bin/pinentry-basic.exe"
```

- generate ssh key:
  - `ssh-keygen -t ed25519 -C "dov@example.com"`
- export public key to github with:
  - `cat ~/.ssh/id_ed25519.pub`

- generate gpg key pair:
  - `gpg --full-generate-key`
- export for github with:
  - gpg --armor --export 00EF4D3F22885E4B
