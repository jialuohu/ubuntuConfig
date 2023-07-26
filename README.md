## Topic

My personal Ubuntu configuration after installation.



## Tools & Applications

### apt essentials

Essential tools to install from `apt`.

```bash
sudo apt update && \
sudo apt upgrade -y && \
sudo apt install -y curl wget build-essential gnome-tweaks flatpak gnome-software-plugin-flatpak openjdk-19-jdk openjdk-11-jdk git gh vim mesa-utils mysql-server&& \
sudo apt autoremove -y
```



### AMD Driver (New)

```bash
# https://www.amd.com/en/support/linux-drivers
amdgpu-install --opencl=rocr --vulkan=amdvlk,pro --accept-eula --no-32 --usecase=graphics
```

To know if the graphic driver is installed correctly

```bash
glxinfo | grep rendering
```





### git & gh

```bash
git config --global user.email "x"
git config --global user.name "x"
gh auth login
```





### flatpak

Applications for daily usage from `flatpak`.

- Add flatpak hub repository

```bash
sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo && \
sudo reboot
```

- Install following applications

```bash
# spotify chrome vscode obs-studio GIMP Flameshot VLC GeoGebra telegram Discord sublime Notepadqq Typora Zoom GnomeExtensionManager Steam qBittorrent Slack
flatpak install -y flathub \
com.spotify.Client com.google.Chrome com.visualstudio.code com.obsproject.Studio org.gimp.GIMP org.flameshot.Flameshot org.videolan.VLC org.geogebra.GeoGebra org.telegram.desktop com.discordapp.Discord com.sublimetext.three com.notepadqq.Notepadqq io.typora.Typora us.zoom.Zoom com.mattjakeman.ExtensionManager com.valvesoftware.Steam org.qbittorrent.qBittorrent com.slack.Slack com.getpostman.Postman
```



### Vim

```bash
cd ~/Downloads && \
git clone https://github.com/jialuohu/vimConfig.git && \
cd vimConfig && \
cp vimrc ~/.vimrc && \
mkdir -p ~/.vim/syntax && \
cp syntax/nginx.vim ~/.vim/syntax/ && \
mkdir -p ~/.vim/plugin && \
cp plugin/auto-pairs.vim ~/.vim/plugin && \
cd ~/Downloads && rm -rf vimConfig
```

`REF:`

- https://github.com/jialuohu/vimConfig



### fcitx5

Chinese input engine configuration.

- Install fcitx5 Chinese-input-engine GUI of fcitx

```bash
sudo apt install -y fcitx5 \
fcitx5-chinese-addons \
fcitx5-frontend-gtk4 fcitx5-frontend-gtk3 fcitx5-frontend-gtk2 \
fcitx5-frontend-qt5
```

- Install dictionaries collected from wiki https://github.com/felixonmars/fcitx5-pinyin-zhwiki/releases

```bash
cd ~/Downloads && \
wget https://github.com/felixonmars/fcitx5-pinyin-zhwiki/releases/download/0.2.4/zhwiki-20230507.dict && \
mkdir -p ~/.local/share/fcitx5/pinyin/dictionaries/ && \
mv zhwiki-20230507.dict ~/.local/share/fcitx5/pinyin/dictionaries/
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
- Search `pinyin` in the text-box of the right panel, `sudo reboot`
- Install styles: https://github.com/tonyfettes/fcitx5-nord

```bash
cd ~/Downloads && \
git clone https://github.com/tonyfettes/fcitx5-nord.git && \
mkdir -p ~/.local/share/fcitx5/themes/ && \
cd fcitx5-nord && \
cp -r Nord-Dark/ Nord-Light/ ~/.local/share/fcitx5/themes/
```

- Enable styles

```bash
vim ~/.config/fcitx5/conf/classicui.conf

    Theme=Nord-Dark
    # or
    Theme=Nord-Light
    
fcitx5 -r
```



`REF:` 

- https://muzing.top/posts/3fc249cf/#fcitx-%E9%85%8D%E7%BD%AE
- https://github.com/felixonmars/fcitx5-pinyin-zhwiki/releases
- https://github.com/tonyfettes/fcitx5-nord



### JetBrains ToolBox

```bash
cd /opt/
# https://www.jetbrains.com/toolbox-app/
sudo tar -xvzf ~/Downloads/jetbrains-toolbox<tab>
sudo mv jetbrains-toolbox<tab> jetbrains
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
sudo usermod -aG docker jerryhu
```

`REF:` 

- https://docs.docker.com/engine/install/ubuntu/



### NVM

`nvm` is a version manager for `node.js`

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash && \
source ~/.bashrc && \
nvm install node
```

`REF:`

- https://github.com/nvm-sh/nvm



### Tomcat10

```bash
cd ~/Downloads && \
wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.9/bin/apache-tomcat-10.1.9.tar.gz && \
tar zxvf apache-tomcat-10.1.9.tar.gz && \
sudo mv apache-tomcat-10.1.9 /opt/tomcat10
```





### Balena Etcher

- Go to https://github.com/balena-io/etcher
- Download from the release repo
- Installation

```bash
# Install using dpkg
sudo dpkg -i balena-etcher_******_amd64.deb
# If you're missing dependencies you can fix them with
sudo apt update && apt --fix-broken install
```

`REF:` 

- https://github.com/balena-io/etcher



## Gnome

### High Resolution Issue with Login Page

 ```bash
 sudo vim /usr/share/glib-2.0/schemas/org.gnome.desktop.interface.gschema.xml
 	<key name="scaling-factor" type="u">
     <default>0</default>
     # to
     <key name="scaling-factor" type="u">
 	<default>2</default>
 sudo glib-compile-schemas /usr/share/glib-2.0/schemas
 ```

Then `sudo reboot` or just log out.









