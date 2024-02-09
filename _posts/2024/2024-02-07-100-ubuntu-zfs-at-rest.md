I have a home storage server with 6 drives in a raidz2 zfs pool, and a seperate boot drive. In case it gets stolen, I want to have all of the data encrypted at rest, but since it's down in the garage I also need to be able to boot into it remotely after a restart without having to hook up a mouse and keyboard.

To do this, I used a fresh install of Ubuntu on the boot drive, selecting 'Encrypt the new Ubuntu installation for security'. This enables LUKS encryption on the boot drive, and every time you restart the system you'll be presented with a splash screen to decrypt the drive before booting into the OS.
The next step is to set up the system to allow remote unlocking via SSH. This is done by installing the `dropbear` package, which is a small SSH server that can be used to unlock the LUKS encrypted drive. The package will install a script that will automatically start the dropbear server when the system boots, and then shut it down after the drive is unlocked.

`sudo apt install dropbear-initramfs`

add your ssh key to `/etc/dropbear/initramfs/authorized_keys`

Now after a restart you can ssh in as root, and run 'cryptroot-unlock' to unlock the drive. This will then shutdown the ssh connection, and after a few seconds you will be able to ssh in again using your regular user account.

Next, I encrypted the zfs pool using native zfs encryption:

`sudo zfs create -o encryption=aes-256-gcm -o keyformat=passphrase storage/photos`

Now, when the system boots, the boot drive will be unlocked via ssh, and then the zfs pool will be unlocked using 'zfs load-key storage/photos' with the passphrase. This means that the entire system is encrypted at rest, and the system can be booted into remotely.


Issues:
As the dropbear server runs its own ssh server, it doesnt know about your regular ssh server or the users on the system. This means that you can only unlock the drive as root, and then you have to log in again as your regular user. This is a bit of a pain, but I haven't found a good way round it yet.


