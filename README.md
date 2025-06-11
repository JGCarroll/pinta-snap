# Pinta as a snap
[![Get it from the Snap Store](https://snapcraft.io/static/images/badges/en/snap-store-black.svg)](https://snapcraft.io/pinta)

Pinta is a freely licensed cross platform drawing application that emulates the functionality of [Paint.NET](https://getpaint.net). 

It's source code is available at https://github.com/PintaProject/Pinta/

# Build Instructions
For most default Ubuntu environments,
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install snapd
sudo snap update
sudo snap install lxd
sudo lxd init --auto
sudo snap install snapcraft --classic
```
In some scenarios, you may need to reboot once to properly initialise LXD and the rest of the snap environment. You may also have to set up your user with the `lxd` group; such as in WSL2 for example, with e.g.,
```
sudo usermod -a -G lxd $USER
```
Often, followed by another reboot (or just the one - if you did this all in one go).

```bash
sudo apt install git
git clone https://github.com/JGCarroll/pinta-snap.git
cd pinta-snap
snapcraft --debug --verbose
```
Snapcraft will automatically set up the entire .NET and Gnome environment and produce the snap with consistent tooling through the LXD backend. You can install your snap with `sudo snap install pinta_myVersion_amd64.snap --dangerous`, using `--dangerous` to skip the signature certificate checks. This is fully equivilent to running Pinta from the official snap store except for the requirement to manually connect the `removable-media` interface on custom versions (`sudo snap connect pinta:removable-media`).

You may want to consider pointing the `snapcraft.yaml` file to your own Github forked repository, or instead copying the `snap` folder in its entireity into the main Pinta repository separately on your local machine, then rewriting the `source:` to be `./` - i.e, the local folder you're operating upon Pinta directly in.
