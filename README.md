# rosa-resolver-patch
The resolver is probably incorrectly configured in the ROSA Linux distribution. To fix the flaw, this rpm-patch was made. Files are replaced during installation:
+ `Network Manager 1.36.6` is installed first
+ `rosa-resolver-patch` is installed next
```
/etc/nsswitch.conf
/etc/systemd/resolved.conf
/run/systemd/resolve/stub-resolv.conf
/etc/NetworkManager/NetworkManager.conf
ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf
systemctl restart NetworkManager systemd-resolved
```
After the uninstall, the files are returned by default.

**Note:** similar files from distributions using `systemd-resolved` (LUbuntu, Mint) were taken as a sample. After installing the patch, `/etc/resolv.conf` starts updating correctly. This allows you to use, for example, Cloudflare (TM) WARP; see [warpgui](https://github.com/AKotov-dev/warpgui).
