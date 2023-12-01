1. `sudo losetup -fP file.img`
	- `-f` - find first unused loopback device
	- `-P` - Scan partition table on newly created loopback device
2. `losetup -a`
	- Find loopback device for `file.img`
3. `ls /dev/loopX*`
	- Find partition device
4. `sudo mount /dev/loopXpY /mount/path`
5. Inspect `/mount/path` to your heart's content
6. `sudo umount /mount/path`
7. `sudo losetup --detach-all`
	- Unmount all loopback devices