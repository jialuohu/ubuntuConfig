## Topic

My personal Ubuntu configuration after installation.



## Tools & Applications

### apt

Essential tools to install from `apt`.

```bash
sudo apt update && \
sudo apt install -y curl wget build-essential gnome-tweaks flatpak gnome-software-plugin-flatpak openjdk-19-jdk openjdk-11-jdk git vim && \
sudo apt upgrade -y && \
sudo apt autoremove -y
```



### flatpak

Applications for daily usage from `flatpak`.

```bash
# Add flatpak hub repository
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
sudo reboot
```

```bash
# spotify chrome vscode obs-studio GIMP Flameshot VLC GeoGebra telegram Discord sublime Notepadqq Typora Zoom GnomeExtensionManager Steam qBittorrent Slack
flatpak install -y flathub \
com.spotify.Client com.google.Chrome com.visualstudio.code org.gimp.GIMP org.flameshot.Flameshot org.videolan.VLC org.geogebra.GeoGebra org.telegram.desktop com.discordapp.Discord com.sublimetext.three com.notepadqq.Notepadqq io.typora.Typora us.zoom.Zoom com.mattjakeman.ExtensionManager com.valvesoftware.Steam org.qbittorrent.qBittorrent com.slack.Slack com.getpostman.Postman
```



### fcitx5

Chinese input engine configuration.

- Install fcitx5 Chinese-input-engine GUI of fcitx

```bash
sudo apt install fcitx5 \
fcitx5-chinese-addons \
fcitx5-frontend-gtk4 fcitx5-frontend-gtk3 fcitx5-frontend-gtk2 \
fcitx5-frontend-qt5
```

- Install dictionaries collected from wiki https://github.com/felixonmars/fcitx5-pinyin-zhwiki/releases

```bash
wget https://github.com/felixonmars/fcitx5-pinyin-zhwiki/releases/download/0.2.4/zhwiki-20220416.dict
mkdir -p ~/.local/share/fcitx5/pinyin/dictionaries/
mv zhwiki-20220416.dict ~/.local/share/fcitx5/pinyin/dictionaries/
```

- Type `im-config` to choose the priority-choice of input engine. Choose `fcitx5` here.
- Write `environment variables` into `~/.bashrc` file.

```bash
export XMODIFIERS=@im=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
```

-  Add `fcitx5` into startup applications of Tweaks `(sudo apt install gnome-tweaks)`
- Configure `fcitx5` by type `fcitx5-configtool`
- Search `pinyin` in the textbox of the right panel
- Install

https://github.com/tonyfettes/fcitx5-nord

 

`REF:` 

- https://muzing.top/posts/3fc249cf/#fcitx-%E9%85%8D%E7%BD%AE



### JetBrains ToolBox

```bash
cd /opt/
# Download the application from https://www.jetbrains.com/toolbox-app/
sudo tar -xvzf ~/Downloads/jetbrains-toolbox
sudo mv jetbrains-toolbox jetbrains
jetbrains/jetbrains-toolbox

# if you cannot open it
(sudo apt install libfuse2)
```



### docker

- Set up repository 

```bash
sudo apt-get update && \
sudo apt-get install ca-certificates curl gnupg && \
sudo install -m 0755 -d /etc/apt/keyrings && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg && \
sudo chmod a+r /etc/apt/keyrings/docker.gpg && \
echo \
"deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
"$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

- Install docker engine

```bash
sudo apt-get update && \
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin && \
sudo docker run hello-world
```

`REF:` https://docs.docker.com/engine/install/ubuntu/



### balena etcher

- Go to https://github.com/balena-io/etcher
- Download from the release repo
- Installation

```bash
# Install using dpkg
sudo dpkg -i balena-etcher_******_amd64.deb
# If you're missing dependencies you can fix them with
sudo apt update && apt --fix-broken install
```





## Gnome

### Tweaks

- Set top bar to have full time & calendar display
- Put `fcitx5` into startup applications
- ...









