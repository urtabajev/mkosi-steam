# Steam in systemd-nspawn container

Created while learning systemd-nspawn and [mkosi](https://0pointer.net/blog/mkosi-a-tool-for-generating-os-images.html).

## Config

* `mkosi.default` holds `Password=`
* `mkosi.postinst` has `USER` (default is steam) for running `steam`

## Usage

* Execute `sudo mkosi boot` in repo root
* Login as `USER` using `Password` value from `mkosi.default`
* Run `steam`

## Remarks

When you are happy with image move `image.{raw,nspawn}` from `mkosi.output` to better location and use with running:
`sudo systemd-nspawn --image=image.raw --settings=trusted`

You may also want to rename `image.raw` and `image.nspawn' to something more meaningful by replacing `image` in both
file names to another string (must be same for both).

### Why some options in mkosi.default not used
* `Repositories=` caused exception (for distros using `apt`, adding multiverse for Arch works fine)
* Section `[Output]` seemed to cause ignoring `[Files]` section in `.nspawn` when `mkosi boot` was used.
