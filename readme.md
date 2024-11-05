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
```