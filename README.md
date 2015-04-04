ansible-swapfile
================

This role configures a swapfile (/swapfile) with the (default) size of 512MB.

## Dependencies

None.

## Variables

* `swapfile_use_dd` [default: `False`]: if set to False, `fallocate` is used to create the swapfile, otherwise, `dd` is used. You may need to set this to True if your filesystem does not support `fallocate` -- see Issue #3.

* `swapfile_size` [default: `512MB`]: the size of the swapfile to create in the format that `fallocate` expects:

    The  length and offset arguments may be followed by binary (2^N) suffixes KiB, MiB, GiB, TiB, PiB and EiB (the "iB" is optional, e.g. "K" has the same meaning as "KiB") or decimal (10^N) suffixes KB, MB, GB, PB and EB.

    If `swapfile_use_dd` is set to True, `swapfile_size` must be set to the amount of megabytes to write, e.g. `512`.

* `swapfile_location` [default: `/swapfile`]: the location of where the swapfile will be created

### Optional

The following variables are set to `False` by default and will not have any effect on your hosts. Setting them to any value other than `False` will update your hosts' sysctl.conf file.

* `swapfile_swappiness` [default: `False`]: the swappiness percentage (vm.swappiness) -- the lower it is, the less your system swaps memory pages

* `swapfile_vfs_cache_pressure` [default: `False`]: "this percentage value controls the tendency of the kernel to reclaim the memory which is used for caching of directory and inode objects."

## Usage

```yaml
- hosts: all
  roles:
    - kamaln7.swapfile
```

or:

```yaml
- hosts: all
  roles:
    - { role: kamaln7.swapfile, swapfile_size: 1GB, swapfile_swappiness: 10, swapfile_location: /mnt/swapfile }
```

You can also set the variables described above in `group_vars` or `host_vars` (see `defaults/main.yml`).

## License

The MIT License (MIT)

Copyright (c) 2014 Kamal Nasser <hello@kamal.io>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
