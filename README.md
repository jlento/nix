# nix

Nix, NixOS and Nixops related experiences

## Installing Nix on OSX

Two extra steps seemed to be necessary on my Mac

.1. Create `/nix`directory

```
    sudo mkdir /nix
    sudo chown $USER /nix
```

.2. Add the following line to `$HOME/.bash_profile

```
    if [ -e $HOME/.nix-profile/etc/profile.d/nix.sh ]; then . $HOME/.nix-profile/etc/profile.d/nix.sh; fi
```

Then the following line installed nix

```
   curl https://nixos.org/nix/install | sh
```

## Installing nixops

In OSX, the packaged version 1.3 fails with virtualbox provider (https://github.com/NixOS/nixops/issues/340). Installing a development version according to https://nixos.org/nixops/manual/#chap-hacking

```
git clone git://github.com/NixOS/nixops.git
cd nixops
nix-build release.nix -A build.x86_64-darvin
nix-shell release.nix -A build.x86_64-darvin --exclude tarball
```

Now having trouble with Host-Only networking. Hope it's only me.

Well, restarting `vboxnet0`helped. Phew.

```
sudo ifconfig vboxnet0 down
sudo ifconfig vboxnet0 up
```


## NixOS desktop VM

Configuration file `desktop.nix`:

```
{
  desktop =
    { deployment.targetEnv = "virtualbox";

     services.xserver.enable = true; 
     services.xserver.displayManager.kdm.enable = true;
     services.xserver.desktopManager.kde4.enable = true;

    };
}

Creating the image and deploying it:

```
nixops create -d desktop desktop.nix
nixops deploy -d desktop
nixops reboot -d desktop
```

```
