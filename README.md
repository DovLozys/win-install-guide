# win-install-guide

some notes on how I do it these days...

## Bootable USB Creation

- Download windows .iso from <https://www.microsoft.com/software-download/windows11>

  - Product Language: en-us
  - verify .iso with `Get-FileHash` in PowerShell

- rufus win experience settings:
  ![Rufus settings](https://github.com/DovLozys/win-install-guide/assets/755086/7b13c307-7127-4329-b55b-aae4448c97f9)

## Windows 11 Installation

After booting into the USB, change Time and currency format to `English (World)` (disables app store, doesn't install other unused apps).

Select Windows edition -> Custom: Install Windows only -> delete all partitions and install to Unallocated Space.

Once file copying is done, restart into bios to check boot order priority is with the fresh Windows drive first.

Once we get to OOBEREGION error, skip that, chose I don't have internet -> Continue with limited setup and installation is done.

## Windows 11 Setup

### Settings

Region -> Country or region -> UK, Regional format -> UK.

Time zone -> London

System -> About -> Rename this PC

### Drivers

Install all device drivers, restarting as required.

Chipset, wifi, bluetooth, integrated graphics, dedicated graphics, sound.

If an error about PieExtension comes up when installing wifi, drop .exe into Extensions folder.

Turn on internet and in admin terminal run `irm "https://christitus.com/win" | iex`, then `Tweaks -> Standard -> Run Tweaks`, then `Run oosu10`.

Run app store updates and windows updates, until no more updates found.

### Control Panel Settings

### Software

Download and install msvcredist, dxwebinstall
TODO: CTT install video summary

## Dev env

### wsl/git

- `wsl --install`

- generate ssh key:
  - `ssh-keygen -t ed25519 -C "dov@example.com"`
- export public key to auth/sign commits in github with:
  - `cat /PATH/TO/.SSH/KEY.PUB`

- .gitconfig:

```bash
git config --global user.email "dov@example.com"
git config --global user.name "Dov"
git config --global gpg.format ssh
git config --global user.signingkey /PATH/TO/.SSH/KEY.PUB
```

### VSCode

- `@tag:telemetry` set to off
- `Enables commit signing with GPG`
- disable restoring of prev open projects
