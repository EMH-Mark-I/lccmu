# lccmu

This is a bash script for the creation of LUKS encrypted file containers. It can also be used to mount and unmount LUKS containers.

#### Requirements

Cryptsetup (LUKS enabled)

Device Mapper 

Linux Unified Key Setup (LUKS)

fallocate

BASH

## Setup

Enable the execute permission bit for the "lccmu" file.

`chmod +x lccmu`

Move lccmu into /bin

`sudo mv lccmu /bin/`

### How to use script

lccmu [OPTION]... [FILE]... [SIZE]...

There are three options. 

`-c | --create` 

`-m | --mount`

`-u | --umount`

• --create container example:

`lccmu -c container1 120M` or `lccmu -c /path/for/container1 120M`

Following the creation of the file, you will be prompted to insert "YES" in capital letters before the file is formatted. If you fail to insert "YES," lccmu will exit and you will be left with a blank file. Lccmu won't be able to continue in the creation of that container and you will have to remove the blank file before starting over.

After inserting "YES" you will be prompted to create a pass-phrase for the container, and to verify the pass-phrase. 

Once the pass-phrase is created, lccmu using cryptsetup will need to open the container in preparation for applying a file-system. This will require elevated permissions to execute, so it may prompt for the sudo user password. It will also prompt you again for the pass-phrase of the container itself.

After applying the filesystem, you should see "LUKS container complete!"

• --mount container example:

`lccmu -m container1`

or

`lccmu -m /path/to/container1`

• --umount container example:

`lccmu -u container1`

or

`lccmu -u /path/to/container1`

## Additional Information

The container size has to be atleast 2.2MB.

Containers are mounted in /media by default. You can edit the first variable in the script line 6, "mntl=/media" to a custom location if you want.

lccmu assumes the active user account that's running the script when mounting the container image so that it can apply the user permissions required for that user to access the container. (If you run lccmu as sudo/root, only the root user will have access to the mounted container.)

You can use spaces for container and directory names, but it would need to be encapsulated in quotes or you could provide a "\" before each space.

You can unmount a container from anywhere on your system so long as you know the containers name. A full path to the image file isn't required when unmounting.

#### Credits

EMH-Mark-I