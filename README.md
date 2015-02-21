# LXC container manager

Small bash script that manages LXC containers, performs operations on one
of container all on all configured containers.

## Prerequisites

All active containers should have:

 1. **User with name same as container name** - *sh* command assumes that all
    containers have user with the same name as container name. Sh commands
    are performed as this user.
 2. **Running ssh server** - *cp* command uses *scp* program to perform
    transfers between containers.

## Installation

Simply download the script and make it an executable file.

```bash
BIN_DIR=~/bin # change this if you want
mkdir -p $BIN_DIR
wget https://github.com/muroc/lxc-tricks/raw/master/container \
  -O $BIN_DIR/container
chmod +x $BIN_DIR/container
```

If BIN_DIR is no on the PATH, modify PATH in rc file of your shell.

```
RC_FILE=~/.bashrc # change if you are not using bash
echo "PATH=$BIN_DIR:$PATH" >> $RC_FILE
. $RC_FILE
```

## Configuration

```bash
cat > ~/.c/defaults << EOF
ACTIVE_CONTAINERS='browser gamedev' # replace with names of your containers
FORCE_TERMINAL='mate-terminal' # change to terminal program you are using
EOF
```

## Usage examples

```bash
container help # prints detailed usage information
container start # starts all active containers
container stop # stops all active containers
container browser sh # starts shell in container browser as users browser
container browser # same as above sh is the default action
```

### Copying files between containers

Following command copies file /home/browser/Downloads/photo.jpg from container
*browser* to container *gamedev* at location */home/gamedev/photo.jpg*:

```bash
container cp browser:Downloads/photo.jpg gamedev:
```

Transfer is done using scp program, so ssh servers running on the containers
are needed to perform the transfer.
