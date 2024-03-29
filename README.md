# Steam in systemd-nspawn container

Created while learning systemd-nspawn and [mkosi](https://0pointer.net/blog/mkosi-a-tool-for-generating-os-images.html).

## Requirements
* Install `mkosi` with `sudo pip3 install git+https://github.com/systemd/mkosi.git` as packaged versions do not support `Environment=` correctly.
* Xorg
* debootstrap
* systemd
* systemd-container
* zstd

## Config

* `mkosi.default` holds `Password=` (default is `steam`)
* `mkosi.default` has `STEAM_HOSTNAME` for container hostname
* `mkosi.default` has `STEAM_USER` (default is `steam`) for running `steam`

## Usage

* Execute `sudo mkosi boot` in repo root
* Login as `STEAM_USER` using `Password` value from `mkosi.default`
* Run `steam`

## Remarks

When you are happy with image move `image.{raw,nspawn}` from `mkosi.output` to better location and use with running:
`sudo systemd-nspawn --image=image.raw --settings=trusted`

You may also want to rename `image.raw` and `image.nspawn` to something more meaningful by replacing `image` in both
file names to another string (must be same for both).

### Why some options in mkosi.default not used
* Section `[Output]` seemed to cause ignoring `[Files]` section in `.nspawn` when `mkosi boot` was used.

## Todo
* Use bind mount for Steam data makinge easier to replace system.
* Bring in systemd-sysext.
