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
sudo wget -P /mnt/etc/nixos/configuration.nix https://raw.githubusercontent.com/andreizpgh/nixos/main/basic-configuration.nix
```

`sudo nixos-install`

`sudo reboot`

### 3. Further configuration

- **Log in as root and set password**
`passwd andrei`

- **Activate an internet connection**
`nmtui`

- **Synchronize "nixos" folder via Syncthing**

- **Rewrite configuration.nix**
```
sudo rm /etc/nixos/configuration.nix && mv /home/andrei/nixos/nixos/configuration.nix /etc/nixos && ln -s /etc/nixos/configuration.nix /home/andrei/nixos/nixos/configuration.nix
```

- **Reboot** 
`sudo reboot`

### 4. Setting-up

- **Command**
```
sudo mkdir /home/andrei/.config/alacritty /home/andrei/.config/nvim /home/andrei/.config/rofi /home/andrei/.config/zathura && rm -rf /home/andrei/nixos/.git && rm /home/andrei/.config/vifm/vifmrc && stow -d /home/andrei/nixos . && chmod +x /home/andrei/.scripts/zettelkasten.sh && sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim' && nix-env -iA nixos.zsh-autosuggestions && nix-env -iA nixos.zsh-syntax-highlighting && lxappearance
``` 
 
- **Log in into Firefox and import 'Scroll Anywhere', 'Vimium' and 'Simple Translate' configs**
