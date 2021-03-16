# Software

### Google Chrome

```text
sudo dnf install -y fedora-workstation-repositories
sudo dnf config-manager --set-enabled google-chrome
sudo dnf install -y google-chrome-stable
```

{% hint style="info" %}
 For self-signed SSH to work locally, enable: `chrome://flags/#allow-insecure-localhost`
{% endhint %}

### Nemo

```text
sudo dnf install -y \
 nemo \
 nemo-fileroller \
 nemo-preview \
 nemo-compare

xdg-mime default nemo.desktop \
 inode/directory \
 application/bzip2 \
 application/gzip \
 application/x-7z-compressed \
 application/x-7z-compressed-tar \
 application/x-bzip \
 application/x-bzip-compressed-tar \
 application/x-compress \
 application/x-compressed-tar \
 application/x-cpio \
 application/x-gnome-saved-search \
 application/x-gzip \
 application/x-lha \
 application/x-lzip \
 application/x-lzip-compressed-tar \
 application/x-lzma \
 application/x-lzma-compressed-tar \
 application/x-tar \
 application/x-tarz \
 application/x-xar \
 application/x-xz \
 application/x-xz-compressed-tar \
 application/zip
```

### Utilities

* lsyncd directory live-sync tool
* meld is a diff merge tool
* pavucontrol audio volume troubleshooting
* pv needed for some bash scripts.
* qt5-qtsvg required for flameshot's icons to work \(since Fedora 30\)
* Remmina: remote desktop software
* ShellCheck is shell code analysis tool, gives great tips, kind of like linting

```text
sudo dnf install -y \
  ack \
  dnf-plugins-core \
  flameshot \
  gnome-tweaks \
  htop \
  jq \
  lsyncd \
  meld \
  util-linux-user \
  nano \
  parallel \
  pavucontrol \
  pv \
  qt5-qtsvg \
  remmina \
  ShellCheck \
  svn \
  tilix
```

### NVM / Node.js

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/$(curl -s https://api.github.com/repos/nvm-sh/nvm/releases/latest | jq -r '.tag_name')/install.sh | bash

# First restart your terminal or you'll get "bash: nvm: command not found..."
nvm install --lts
```

{% embed url="https://github.com/nvm-sh/nvm\#install--update-script" %}

### Yarn

```bash
curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
sudo dnf install -y yarn
```

### Dropbox

Get latest download link from [https://www.dropbox.com/install-linux](https://www.dropbox.com/install-linux).

```bash
wget https://www.dropbox.com/download?dl=packages/fedora/nautilus-dropbox-2020.03.04-1.fedora.x86_64.rpm -O ~/Downloads/dropbox.fedora.rpm
sudo dnf install -y ~/Downloads/dropbox.fedora.rpm
```

Open Dropbox, follow prompt that will install the daemon. Once complete you will be prompted to log in to Dropbox

### SSH Keys

```text
mkdir ~/.ssh
sudo chmod 700 ~/.ssh
# Copy keys from Bitwarden ("SSH Keys")
# chmod private keys to 600, public keys to 644
sudo chmod 600 ~/.ssh/2018.07.curtisbelt
sudo chmod 644 ~/.ssh/2018.07.curtisbelt.pub
ssh-add ~/.ssh/2018.07.curtisbelt
```

### Oh My ZSH

```text
sudo dnf -y install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

* Reboot computer
* Warning: If you already cloned in your dotfiles and ran `make`, you'll want to `sudo rm -R ~/.oh-my-zsh`, install, then go run `make` again. Or just don't setup your dotfiles until after installing oh-my-zsh.

{% hint style="danger" %}
**Below this point: working on fixing formatting**
{% endhint %}

```text
Dotfiles
```

* ```text
  mkdir -p ~/code/github.com/curtisbelt/dotfiles
  git clone git@github.com:curtisbelt/dotfiles.git ~/code/github.com/curtisbelt/dotfiles
  cd ~/code/github.com/curtisbelt/dotfiles
  make
  sudo chown 600 ~/code/github.com/curtisbelt/dotfiles/home/.ssh/config
  ```
* Software Installers available after dotfiles

  ```text
  update-aws-iam-authenticator
  update-bitwarden
  update-dbeaver
  update-discord
  update-docker-compose
  update-docker-ecs
  update-gitkraken
  update-insomnia
  update-slack
  update-terraform
  update-vagrant
  update-wp-cli
  update-yq
  update-zoom
  ```

* Visual Studio Code

  ```text
  sudo rpm --import <https://packages.microsoft.com/keys/microsoft.asc>
  sudo sh -c 'echo -e "[code]\\nname=Visual Studio Code\\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\\nenabled=1\\ngpgcheck=1\\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
  sudo dnf check-update
  sudo dnf install -y code
  ```

* fakexrandr \(Allows splitting ultra-wide monitor into two virtual displays\)

  * From this github comment: [https://github.com/phillipberndt/fakexrandr/issues/28\#issuecomment-169994770](https://github.com/phillipberndt/fakexrandr/issues/28#issuecomment-169994770)
    * Create file `/etc/ld.so.conf.d/aaaaa.conf` with contents `/usr/local/lib/fakexrandr` **\(should be in dotfiles already\)**
    * Create directory `/usr/local/lib/fakexrandr/` **\(should be in dotfiles already\)**

  ```text
  sudo dnf install -y libXrandr-devel libXinerama-devel
  mkdir -p ~/code/github.com/phillipberndt/fakexrandr
  git clone <https://github.com/phillipberndt/fakexrandr.git> ~/code/github.com/phillipberndt/fakexrandr
  cd ~/code/github.com/phillipberndt/fakexrandr
  make && sudo make install
  # Then, run `fakexrandr-manage` to open the GUI - create display, click on rectangle to draw the split screens.
  fakexrandr-manage
  ```

  * LIMITATIONS:
    * Setting primary monitor doesn't work, primary will have to be one of the real monitors.
    * Full screen on video players in Chrome are shifted to the right 50% off screen

* myrepos
  * sudo dnf install -y myrepos
  * 
* Install libxcrypt-compat [https://github.com/hashicorp/vagrant/issues/10830\#issuecomment-490881987](https://github.com/hashicorp/vagrant/issues/10830#issuecomment-490881987)
  * sudo dnf install -y libxcrypt-compat
* * entr - Run arbitrary commands when files change
  * sudo dnf install -y entr
* Android Studio
* OpenJDK
  * sudo dnf install -y java-1.8.0-openjdk-devel.x86\_64 java-11-openjdk-devel.x86\_64 java-latest-openjdk-devel.x86\_64
  * To switch between versions:
    * sudo alternatives --config java
* Code Sniffer
  * composer g require --dev automattic/vipwpcs dealerdirect/phpcodesniffer-composer-installer phpcompatibility/php-compatibility
  * * Old
    * composer global require squizlabs/php\_codesniffer
    * composer global require wp-coding-standards/wpcscomposer
    * composer global require dealerdirect/phpcodesniffer-composer-installer
* Manual Settings - haven't looked at how to progmatically configure
  * Nautilus
    * List view, 50% zoom
    * Show hidden files
    * Sort folders before files
    * Create bookmarks for ~/Github ~/Dropbox ~/WordPress
  * Keyboard Shortcuts
    * Print: flameshot gui
    * Super + E: nautilus
    * Super + T: tilix
  * Gnome-Tweak
    * Disable Caps Lock \(frees up key for PTT binding\)
  * Tilix
    * Global
      * Turn onv: Automatically copy text to clipboard when selection
    * Profiles
      * Font: Hack Regular 9px
    * Color
      * Color scheme: Orchis
  * VSCode
    * ext install shan.code-settings-sync
    * command pallete: Sync: Download Settings
      * enter github token \(should have a gist-only personal access token\)
      * enter gist id \(should have existing private gist with your settings\)
* Qogir Theme
  * git clone [https://github.com/vinceliuice/Qogir-theme](https://github.com/vinceliuice/Qogir-theme) ~/Downloads/Qogir-theme
  * cd ~/Downloads/Qogir-theme
  * bash [install.sh](http://install.sh)
  * gsettings set org.gnome.desktop.wm.preferences button-layout appmenu:minimize,maximize,close
  * 
* gsettings
  * gsettings set org.gtk.Settings.FileChooser show-hidden true
  * gsettings set org.gnome.desktop.interface clock-format '12h'
  * gsettings set org.gnome.desktop.interface clock-show-date true
  * gsettings set org.gnome.desktop.interface clock-show-seconds true
  * gsettings set org.gnome.desktop.interface clock-show-weekday true
  * gsettings set org.gnome.desktop.interface cursor-theme 'Adwaita'
  * gsettings set org.gnome.desktop.interface document-font-name 'Akzidenz-Grotesk BQ Light with Light 11'
  * gsettings set org.gnome.desktop.interface enable-animations true
  * gsettings set org.gnome.desktop.interface font-name 'Akzidenz-Grotesk BQ Light with Light 11'
  * gsettings set org.gnome.desktop.interface gtk-theme 'Qogir'
  * gsettings set org.gnome.desktop.interface menubar-detachable false
  * gsettings set org.gnome.desktop.interface monospace-font-name 'Dank Mono 11'
  * gsettings set org.gnome.desktop.interface toolbar-icons-size 'small'
* NVIDIA \(**ONLY IF YOU HAVE NVIDIA CARD**\)

  ```text
  sudo dnf install -y <https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-33.noarch.rpm> <https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-33.noarch.rpm>
  sudo dnf update -y
  sudo dnf install -y akmod-nvidia xorg-x11-drv-nvidia-cuda vdpauinfo libva-vdpau-driver libva-utils
  ```

* Papirus Icon Theme
  * sudo dnf install -y papirus-icon-theme
  * activate in gnome-tweak-tool
* Capitaine Cursors
  * git clone [https://github.com/keeferrourke/capitaine-cursors](https://github.com/keeferrourke/capitaine-cursors) ~/.icons/capitaine-cursors
  * cp -r ~/.icons/capitaine-cursors/dist ~/.icons/capitaine-cursors-black
  * cp -r ~/.icons/capitaine-cursors/dist-white ~/.icons/capitaine-cursors-white
  * activate in gnome-tweak-tool
* Gitkraken
  * cd ~/Downloads && wget [https://release.gitkraken.com/linux/gitkraken-amd64.rpm](https://release.gitkraken.com/linux/gitkraken-amd64.rpm)
  * sudo dnf install -y ./gitkraken-amd64.rpm
  * rm ~/Downloads/gitkraken-amd64.rpm
  * They have an official snap package but it wasn't working \(wouldn't open -- behavior reported by others too\). Maybe try again in the futuresudo snap install gitkrakensudo snap remove gitkraken
* Clone in dot files, run `./make`
* Typora
  * [https://github.com/RPM-Outpost/typora](https://github.com/RPM-Outpost/typora)
* Sublime Text
  * sudo rpm -v --import [https://download.sublimetext.com/sublimehq-rpm-pub.gpg](https://download.sublimetext.com/sublimehq-rpm-pub.gpg)
  * sudo dnf config-manager --add-repo [https://download.sublimetext.com/rpm/stable/x86\_64/sublime-text.repo](https://download.sublimetext.com/rpm/stable/x86_64/sublime-text.repo)
  * sudo dnf check-update
  * sudo dnf install -y sublime-text
* DBeaver
  * cd ~/Downloads && wget [https://dbeaver.io/files/dbeaver-ce-latest-stable.x86\_64.rpm](https://dbeaver.io/files/dbeaver-ce-latest-stable.x86_64.rpm)
  * sudo dnf install -y ./dbeaver-ce-latest-stable.x86\_64.rpm
  * rm ~/Downloads/dbeaver-ce-latest-stable.x86\_64.rpm
* Portainer \(Docker Web Client\)
  * docker volume create portainer\_data
  * docker run -d -p 8000:8000 -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer\_data:/data portainer/portainer
  * Go to [http://localhost:9000](http://localhost:9000)
* Zoom Screen Share
  * cd ~/Downloads && wget [https://zoom.us/client/latest/zoom\_x86\_64.rpm](https://zoom.us/client/latest/zoom_x86_64.rpm)
  * sudo dnf install -y ./zoom\_x86\_64.rpm
  * rm ~/Downloads/zoom\_x86\_64.rpm
* Baremetal LEMP Stack
  * Fedora 28+ doesn't need extra repos
  * Stop the built-in apache \(already stopped/disabled in Fedora 29 but doesn't hurt make sure\)
    * sudo systemctl stop httpd
    * sudo systemctl disable httpd
  * NGINX
    * sudo dnf install -y nginx
    * sudo mkdir -p /var/cache/nginx
    * sudo chown curtis: /var/cache/nginx
    * sudo mkdir -p /var/lib/nginx
    * sudo chown -R curtis: /var/lib/nginx
    * sudo chown -R curtis: /var/log/nginx
    * sudo systemctl start nginx
    * sudo systemctl enable nginx
    * SSL GUIDE

      * [generate-cert.sh](http://generate-cert.sh) \(from dotfiles\)

      ```text
      #!/bin/bashset -eif [ -z "$1" ]; then hostname="$HOSTNAME"else hostname="$1"filocal_openssl_config="[ req ]prompt = nodistinguished_name = req_distinguished_namex509_extensions = san_self_signed[ req_distinguished_name ]CN=$hostname[ san_self_signed ]subjectAltName = DNS:$hostname, DNS:localhostsubjectKeyIdentifier = hashauthorityKeyIdentifier = keyid:always,issuerbasicConstraints = CA:truekeyUsage = nonRepudiation, digitalSignature, keyEncipherment, dataEncipherment, keyCertSign, cRLSignextendedKeyUsage = serverAuth, clientAuth, timeStamping"openssl req \\ -newkey rsa:2048 -nodes \\ -keyout "$hostname.key.pem" \\ -x509 -sha256 -days 3650 \\ -config <(echo "$local_openssl_config") \\ -out "$hostname.cert.pem"openssl x509 -noout -text -in "$hostname.cert.pem"
      ```

      * Chrome:
        * chrome://flags/\#allow-insecure-localhost
        * Enable it, restart chrome.
  * PHP-FPM
    * sudo dnf install -y php-fpm php-common php-opcache php-pecl-apcu php-cli php-pear php-pdo php-mysqlnd php-pgsql php-pecl-mongodb php-pecl-redis php-pecl-memcache php-pecl-memcached php-gd php-mbstring php-mcrypt php-xml php-odbc php-pspell php-soap php-xmlrpc php-zip php-xdebug php-pecl-imagick php-intl
    * sudo mkdir -p /var/log/php-fpm
    * sudo chown -R curtis: /var/log/php-fpm
    * sudo systemctl start php-fpm
    * sudo systemctl enable php-fpm
    * sudo chown curtis: /etc/php.ini
  * MariaDB
    * sudo dnf install -y mariadb-server
    * sudo systemctl start mariadb
    * sudo systemctl enable mariadb
    * sudo mysql\_secure\_installation \(set root pass to "root"\)
* Blackfire
  * Configuring the repository
    * wget -O - "[http://packages.blackfire.io/fedora/blackfire.repo](http://packages.blackfire.io/fedora/blackfire.repo)" \| sudo tee /etc/yum.repos.d/blackfire.repo
    * sudo dnf check-update
  * sudo dnf install -y blackfire-agent blackfire-php
  * Configure the **local agent** with your **personnal server credentials**:
    * sudo blackfire-agent --register --server-id=&lt;SERVER ID&gt; --server-token=&lt;SERVER TOKEN&gt;
  * sudo /etc/init.d/blackfire-agent start
  * sudo systemctl restart blackfire-agent nginx php-fpm
  * 
* WP-CLI
  * sudo dnf install -y wp-cli
  * old way
    * cd /tmp
    * curl -O [https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar](https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar)
    * php wp-cli.phar --info
    * chmod +x wp-cli.phar
    * sudo mv wp-cli.phar /usr/local/bin/wp
    * wp --info
* Update Composer
  * cd /tmp
  * curl -sS [https://getcomposer.org/installer](https://getcomposer.org/installer) \| php
  * sudo mv composer.phar ~/code/github.com/curtisbelt/dotfiles/root/usr/local/bin/composer
  * sudo chmod +x ~/code/github.com/curtisbelt/dotfiles/root/usr/local/bin/composer
* AWS CLI / EB CLI
  * pip3 install awscli --upgrade --user
  * pip3 install awsebcli --upgrade --user
  * aws configure
    * enter key and secret
    * region: us-east-1
    * format: json
    * code commit: N
* Setup WordPress
  * mkdir ~/WordPress
  * cd ~/WordPress
  * wp core download
  * export WORDPRESS\_DB\_NAME=vanilla
  * export DOMAIN\_CURRENT\_SITE=vanilla.localhost
  * wp db create --url=vanilla.localhost
  * export IS\_SINGLE\_SITE=true
  * wp core multisite-install --subdomains --skip-config --skip-email --title=Vanilla --admin\_user=curtis --admin\_password=curtis --admin\_email=curtis@curtisbelt.dev --url=vanilla.localhost
  * export IS\_SINGLE\_SITE=false
  * wp plugin install wp-seo-qtranslate-x acf-qtranslate toolbar-publish-button kint-debugger acf-content-analysis-for-yoast-seo amazon-s3-and-cloudfront duplicate-post wordpress-seo classic-editor classic-editor-addon --activate-network --url=awswp.localhost
  * bash ~/Github/CurtisBelt/dotfiles/scripts/git-repos.sh
  * Permissions
    * nginx and php-fpm should be configured to run by `curtis`
    * sudo find ~/WordPress/ -type d -exec chmod 755 {} \;
    * sudo find ~/WordPress/ -type f -exec chmod 664 {} \;
    * sudo chmod -R 775 ~/WordPress/wp-content
    * sudo find /efs -type d -exec chmod 775 {} \;
    * sudo chmod -R 775 /efs



* Increase inotify limit -- Specifically Gitkrakken would hit a limit, but this applies to everything using inotify such as webpack, grunt, VSCode -anything watch files for changes.
  * echo fs.inotify.max\_user\_watches=524288 \| sudo tee /etc/sysctl.d/40-max-user-watches.conf && sudo sysctl --system



* Fsearchhttps://github.com/cboxdoerfer/fsearch/wiki/Build-instructions
  * sudo dnf install -y automake autoconf intltool libtool autoconf-archive pkgconfig glib2-devel gtk3-devel git
  * mkdir -p ~/code/github.com/cboxdoerfer
  * git clone [https://github.com/cboxdoerfer/fsearch.git](https://github.com/cboxdoerfer/fsearch.git) ~/code/github.com/cboxdoerfer/fsearch
  * cd ~/code/github.com/cboxdoerfer/fsearch
  * ./autogen.sh
  * ./configure
  * make && sudo make install
* Peek
  * sudo dnf install -y [https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-33.noarch.rpm](https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-33.noarch.rpm) [https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-33.noarch.rpm](https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-33.noarch.rpm)
    * sudo dnf install -y ffmpeg gstreamer1-plugins-ugly
  * sudo dnf install -y peek
* Insomnia
  * Download rpm from [https://github.com/getinsomnia/insomnia/releases/latest](https://github.com/getinsomnia/insomnia/releases/latest)
    * curl -L $\(curl -sL [https://api.github.com/repos/getinsomnia/insomnia/releases/latest](https://api.github.com/repos/getinsomnia/insomnia/releases/latest) \| jq -r '.assets\[\]\|select\(.browser\_download\_url \| test\("x86\_64.rpm$"\)\).browser\_download\_url'\) &gt; ~/Downloads/insomnia-latest.rpm
  * sudo dnf install -y ~/Downloads/insomnia-latest.rpm
  * rm ~/Downloads/insomnia-latest.rpm
* Postman
  * curl -L [https://dl.pstmn.io/download/latest/linux64](https://dl.pstmn.io/download/latest/linux64) &gt; ~/Downloads/postman-latest.tar.gz
  * sudo tar xvzf ~/Downloads/postman-latest.tar.gz -C /usr/share
  * sudo ln -s /usr/share/Postman/app/Postman /usr/local/bin/postman
* VLC Player
  * sudo dnf install -y [https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-33.noarch.rpm](https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-33.noarch.rpm) [https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-33.noarch.rpm](https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-33.noarch.rpm)
  * sudo dnf install -y vlc
* Support Video Thumbnails
  * sudo dnf install -y gstreamer1-libav ffmpegthumbnailer
* Spotify

  ```text
  sudo dnf config-manager --add-repo=https://negativo17.org/repos/fedora-spotify.repo
  sudo dnf install -y spotify-client
  ```

* Troubleshooting
  * GUI for Users and Groups
    * sudo dnf install -y system-config-users
  * GUI for ACL Permissions
    * sudo dnf install -y eiciel
  * GUI for dconf database
    * sudo dnf install -y dconf-editor
* Gnome Extensions

  * Just use the chrome extension to install these, it works fine.
  * [https://extensions.gnome.org/extension/545/hide-top-bar/](https://extensions.gnome.org/extension/545/hide-top-bar/)

* Open Broadcaster Software \(OBS\) Project
  * sudo dnf install -y [https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-32.noarch.rpm](https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-32.noarch.rpm) [https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-32.noarch.rpm](https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-32.noarch.rpm)
  * sudo dnf install -y obs-studio
  * NVIDIA only:
    * sudo dnf install -y xorg-x11-drv-nvidia-cuda
* Docker

  * Install using the repository to get latest version

    * Starting with Fedora 32, firewalld uses nftables instead of iptables - this breaks networking in docker-compose. Maybe check if its fixed in the future, but doesn't really matter, no impact on me to go back to iptables...

    ```text
    # Result: FirewallBackend=nftables
    sudo cat /etc/firewalld/firewalld.conf | grep FirewallBackend=
    # Let's go back to iptables
    sudo sed -i 's/FirewallBackend=nftables/FirewallBackend=iptables/g' /etc/firewalld/firewalld.conf
    # Result: FirewallBackend=iptables
    sudo cat /etc/firewalld/firewalld.conf | grep FirewallBackend=
    ```

  * Install Docker

    ```text
    sudo dnf config-manager --add-repo <https://download.docker.com/linux/fedora/docker-ce.repo>
    sudo dnf config-manager --set-enabled docker-ce-test
    sudo dnf install docker-ce docker-ce-cli containerd.io
    sudo systemctl start docker
    sudo systemctl enable docker
    ```

  * Install docker compose

  ```text
  update-docker-compose # from dotfiles
  ```

  * Add $USER to docker group

    ```text
    sudo usermod -aG docker $USER
    newgrp docker
    ```

* * Ansible
  * sudo dnf install -y ansible
* Gimp \(and Batch Processing\)
  * sudo dnf install -y gimp gimp-dbp
* Skype
  * cd /tmp
  * wget --trust-server-names [https://go.skype.com/skypeforlinux-64.rpm](https://go.skype.com/skypeforlinux-64.rpm)
  * sudo dnf install -y /tmp/skypeforlinux-64.rpm
* Varying Vagrant Vagrants
  * Vagrant + Virtualbox
    * cd /etc/yum.repos.d/
    * sudo wget [http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repoz](http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repoz) d
    * sudo dnf update
    * sudo dnf -y install VirtualBox
    * update-vagrant \(from dotfiles\)
    * * vagrant-libvirt needs a new release, until that happens, must manually remove and then re-build from upstream.The issue is fog-core dependency issue when trying to run `vagrant plugin install vagrant-hostsupdater`
      * sudo dnf -y remove vagrant-libvirt rubygem-fog-core
      * sudo dnf -y install qemu libvirt libvirt-devel ruby-devel gcc
      * CONFIGURE\_ARGS="with-libvirt-include=/usr/include/libvirt with-libvirt-lib=/usr/lib64" vagrant plugin install vagrant-libvirt
      * CONFIGURE\_ARGS="with-libvirt-include=/usr/include/libvirt with-libvirt-lib=/usr/lib64" vagrant plugin install vagrant-hostsupdater --local
      * CONFIGURE\_ARGS="with-libvirt-include=/usr/include/libvirt with-libvirt-lib=/usr/lib64" vagrant plugin install vagrant-scp
  * VVV
    * git clone -b master git://github.com/Varying-Vagrant-Vagrants/VVV.git ~/vagrant-local && cd ~/vagrant-local
    * vagrant plugin install vagrant-hostsupdater --local
    * vagrant up --provision
  * PMC-VVV
    * cd ~/vagrant-local
    * bash ~/code/github.com/penske-media-corp/pmc-vvv/build-me-vvv.sh
    * 
* Possible Bluetooth improvement?
  * sudo dnf install pulseaudio-module-bluetooth-freeworld --allowerasing
  * pulseaudio -k
* VIP Go Cli
  * On Nodejs 12
  * npm i -g @automattic/vip-go-internal-cli
  * vipgo config set PROXY=socks://127.0.0.1:8080
  * vipgo login
  * \(get ID and token from [https://admin.wpvip.com/\#/users/347/curtisbelt](https://admin.wpvip.com/#/users/347/curtisbelt)\)
  * npm install -g @automattic/vip
  * vip
* VIP Sandbox Helper
  * Saving hosts file changes without requiring password
    * sudo visudo
    * curtis ALL = \(root\) NOPASSWD: /home/curtis/code/github.com/automattic/vip-sandbox-helper/bin/edit-hosts
* VIP Proxy
  * gsettings set org.gnome.system.proxy mode 'auto'
  * gsettings set org.gnome.system.proxy autoconfig-url '[https://pac.a8c.com/](https://pac.a8c.com/)'
* Bluetooth Setup w/ Windows

  [https://unix.stackexchange.com/questions/255509/bluetooth-pairing-on-dual-boot-of-windows-linux-mint-ubuntu-stop-having-to-p](https://unix.stackexchange.com/questions/255509/bluetooth-pairing-on-dual-boot-of-windows-linux-mint-ubuntu-stop-having-to-p)

  ```text
  cd /run/media/curtis/4C4E57664E5747BA/Windows/System32/config
  chntpw -e SYSTEM
  > cd ControlSet001\\Services\\BTHPORT\\Parameters\\Keys
  (...)\\Services\\BTHPORT\\Parameters\\Keys> ls

  Node has 1 subkeys and 0 values
    key name
    <ac12039fde0d>

  (...)\\Services\\BTHPORT\\Parameters\\Keys> cd ac12039fde0d
  (...)\\BTHPORT\\Parameters\\Keys\\ac12039fde0d> ls

  Node has 0 subkeys and 1 values
    size     type              value name             [value if type DWORD]
      16  3 REG_BINARY         <2811a549782e>

  (...)\\BTHPORT\\Parameters\\Keys\\ac12039fde0d> hex 2811a549782e

  Value <2811a549782e> of type REG_BINARY (3), data length 16 [0x10]
  :00000  A1 19 20 A0 31 1C 11 EC 64 EA B5 64 30 6F 25 3B .. .1...d..d0o%;
  ```

  `sudo nano /var/lib/bluetooth/AC:12:03:9F:DE:0D/28:11:A5:49:78:2E/info`

  ```text
  [LinkKey]
  Key=A11920A0311C11EC64EAB564306F253B
  ```

  `sudo systemctl restart bluetooth`

