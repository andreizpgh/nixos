# Nixos Installation

### 1. Partitioning

| Partition | File System | Label | Size | Flags |
| --------- | ----------- | ----- | ---- | ----- |
| /dev/sda1 | linux-swap  | swap  | 2048 | –     |
| /dev/sda2 | ext4        | msdos | –    | boot  |

### 2. Nixos configuration

`sudo mount /dev/disk/by-label/msdos /mnt`

`sudo nixos-generate-config --root /mnt`

```
nix-env -iA nixos.wget && sudo rm /mnt/etc/nixos/configuration.nix && sudo wget -P /mnt/etc/nixos https://raw.githubusercontent.com/andreizpgh/nixos/main/basic-configuration.nix && sudo rename /mnt/etc/nixos/basic-configuration.nix /mnt/etc/nixos/configuration.nix
```

`sudo nixos-install`

`sudo poweroff`

### 3. Further configuration

- **Log in as root and set password**
`passwd andrei`

- **Log in as 'andrei'**

- **Activate an internet connection**
`nmtui`

- **Synchronize "nixos" and "Org" folders via Syncthing (ID –> tdesktop)**
`mkdir /home/andrei/nixos /home/andrei/Org`

- **Rewrite configuration.nix**
```
sudo rm /etc/nixos/configuration.nix && sudo ln -s /home/andrei/nixos/nixos/configuration.nix /etc/nixos/configuration.nix && rm /home/andrei/nixos/nixos/hardware-configuration.nix && sudo mv /etc/nixos/hardware-configuration.nix /home/andrei/nixos/nixos && sudo ln -s /home/andrei/nixos/nixos/hardware-configuration.nix /etc/nixos/hardware-configuration.nix
```

- **Rebuild** 
`sudo nixos-rebuild switch`

- **Log out and log in again**

### 4. Setting-up

- **Command**
```
sudo mkdir /home/andrei/.config/alacritty /home/andrei/.config/nvim /home/andrei/.config/rofi /home/andrei/.config/zathura && rm /home/andrei/.config/vifm/vifmrc /home/andrei/.config/qtile/config.py && stow -d /home/andrei/nixos . && chmod +x /home/andrei/.scripts/zettelkasten.sh && sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim' && nix-env -iA nixos.zsh-autosuggestions && nix-env -iA nixos.zsh-syntax-highlighting && lxappearance
``` 

- **Install Doom Emacs**
```
git clone https://github.com/hlissner/doom-emacs ~/.emacs.d && yes | ~/.emacs.d/bin/doom install && rm /home/andrei/.doom.d/config.el /home/andrei/.doom.d/init.el /home/andrei/.doom.d/packages.el && ln -s /home/andrei/nixos/nixos/config.el /home/andrei/.doom.d/config.el && ln -s /home/andrei/nixos/nixos/custom.el /home/andrei/.doom.d/custom.el && ln -s /home/andrei/nixos/nixos/init.el /home/andrei/.doom.d/init.el && ln -s /home/andrei/nixos/nixos/packages.el /home/andrei/.doom.d/packages.el && ~/.emacs.d/bin/doom sync
```
 
- **Log in into Firefox and import 'Scroll Anywhere', 'Vimium' and 'Simple Translate' configs**
