```
# Flatpaks

flatpak install flathub com.bitwarden.desktop -y
flatpak install flathub md.obsidian.Obsidian -y
flatpak install flathub org.standardnotes.standardnotes -y
flatpak install flathub com.visualstudio.code -y
flatpak install flathub org.gimp.GIMP -y
flatpak install flathub org.kde.krita -y
flatpak install flathub com.github.PintaProject.Pinta -y
flatpak install flathub be.alexandervanhee.gradia -y
flatpak install flathub com.obsproject.Studio -y
flatpak install flathub org.videolan.VLC -y
flatpak install flathub fr.handbrake.ghb -y
flatpak install flathub org.openshot.OpenShot -y
flatpak install flathub org.localsend.localsend_app -y
flatpak install flathub org.cryptomator.Cryptomator -y
flatpak install flathub com.moonlight_stream.Moonlight -y
flatpak install flathub org.godotengine.Godot -y
flatpak install flathub com.bambulab.BambuStudio -y
flatpak install flathub io.missioncenter.MissionCenter -y
flatpak install flathub org.gnome.Extensions -y
```

```
# Google Chrome

sudo dnf config-manager --enable google-chrome

sudo dnf install google-chrome-stable
```

```
# Tailscale

sudo dnf config-manager addrepo --from-repofile=https://pkgs.tailscale.com/stable/fedora/tailscale.repo
sudo dnf install tailscale

sudo systemctl enable --now tailscaled

tailscale systray
tailscale configure systray --enable-startup=freedesktop

sudo tailscale up
```

```
# Ghostty

sudo dnf copr enable scottames/ghostty
sudo dnf install ghostty
```

```
# Zed

curl -f https://zed.dev/install.sh | sh
```

```
# Docker

sudo dnf -y install dnf-plugins-core
sudo dnf-3 config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo

sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo systemctl enable --now docker
```

```
# Claude Code

curl -fsSL https://claude.ai/install.sh | bash
```

```
# Local AI

curl -LsSf https://llama.app/install.sh | sh

curl -fsSL https://pi.dev/install.sh | sh

curl -fsSL https://herdr.dev/install.sh | sh
```

```
# Microsoft Fonts

sudo dnf install curl cabextract xorg-x11-font-utils mkfontscale fontconfig cpio unzip

curl -fLO https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm

(
    set -euo pipefail

    rpmfile="$PWD/msttcore-fonts-installer-2.6-1.noarch.rpm"
    workdir=$(mktemp -d)
    trap 'rm -rf "$workdir"' EXIT

    fontdir="$HOME/.local/share/fonts/microsoft-core"
    mkdir -p "$fontdir"

    cd "$workdir"
    rpm2cpio "$rpmfile" | cpio -id --quiet
    ./usr/lib/msttcore-fonts-installer/refresh-msttcore-fonts.sh -F "$fontdir"
    for required_font in arial.ttf calibri.ttf; do
        if [ ! -s "$fontdir/$required_font" ]; then
            printf 'Missing expected font: %s\n' "$required_font"
            exit 1
        fi
    done
    fc-cache -f "$fontdir"
)
```

```
# LibreOffice

sudo dnf group remove libreoffice
sudo dnf remove libreoffice*

flatpak install flathub org.libreoffice.LibreOffice -y
```

```
# Virtualisation

sudo dnf install -y qemu-kvm libvirt virt-install bridge-utils virt-manager

sudo dnf install -y libvirt-devel virt-top libguestfs-tools guestfs-tools

sudo systemctl start libvirtd
```

```
# Optional

flatpak install flathub org.onlyoffice.desktopeditors -y
flatpak install flathub com.heroicgameslauncher.hgl -y
flatpak install flathub com.getpostman.Postman -y
flatpak install flathub org.audacityteam.Audacity -y
flatpak install flathub fr.natron.Natron -y
flatpak install flathub io.github.ilya_zlobintsev.LACT -y
flatpak install flathub org.filezillaproject.Filezilla -y
sudo dnf install ulauncher
sudo dnf install steam -y
sudo dnf install ./insync-x.x.x.xxxxx-fc42.x86_64.rpm
sudo dnf install fastfetch
sudo dnf install git-all
sudo dnf install nodejs
```

```
# AI Models

llama serve -hf ggml-org/Qwen3.8-27B-GGUF:Q8_0
```

https://extensions.gnome.org/extension/615/appindicator-support/
