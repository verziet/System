# NixOS configuration and dotfiles reproduction

## Installation
- [NixOS iso](https://nixos.org/download/)

After creating, formatting and mounting a boot and root partition with an optional swap partition
```bash
sudo nixos-generate-config --root /mnt # generate hardware specific config
cd /mnt/etc/nixos
nix-shell -p git # required to clone the repo and build the system using flakes
sudo git clone https://github.com/verziet/System.git
sudo cp hardware-configuration.nix System/nixos # flake.nix looks for nixos/hardware-configuation.nix
# change username and hostname in flake.nix and nixos/configuration.nix
sudo nixos-install --flake ./System#hostname # install using the flake, replace hostname
reboot # boot into NixOS, grub should work now
# grub won't find any Windows entries yet, will fix soon
# we need to change user's password now
su - # switch to root
passwd username # set password for user, replace username
exit # go back to user account
sudo mv /etc/nixos/System $HOME # move System directory to home directory for easier access
sudo nixos-rebuild switch --flake ./System#hostname # this fixes the grub Windows entries
```