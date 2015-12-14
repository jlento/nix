# nix

Nix, NixOS and Nixops related experiences

## Installing Nix on OSX

Two extra steps seemed to be necessary on my Mac

1. Create `/nix`directory

    sudo mkdir /nix
    sudo chown $USER /nix

2. Add the following line to `$HOME/.bash_profile

    if [ -e $HOME/.nix-profile/etc/profile.d/nix.sh ]; then . $HOME/.nix-profile/etc/profile.d/nix.sh; fi

Then the following line installed nix

    curl https://nixos.org/nix/install | sh

## Installing nixops

In OSX,

    nix-channel --add http://nixos.org/channels/nixpkgs-unstable
    nix-channel --update
    nix-env -i nixops


