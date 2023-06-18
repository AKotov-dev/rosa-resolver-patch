# rosa-resolver-patch
The resolver is probably incorrectly configured in the ROSA Linux distribution. To fix the flaw, this rpm-patch was made. Files are replaced during installation:
```
/etc/nsswitch.conf
/etc/systemd/resolved.conf
/etc/NetworkManager/NetworkManager.conf
```
After the uninstall, the files are returned by default.

**Note:** similar files from distributions using `systemd-resolved` (Lubuntu, Mint) were taken as a sample. After installing the patch, `/etc/resolv.conf` starts updating correctly. This allows you to use, for example, Cloudflare (TM) WARP; see [warpgui](https://github.com/AKotov-dev/warpgui).
