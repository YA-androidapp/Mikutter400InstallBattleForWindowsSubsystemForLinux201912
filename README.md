# Mikutter400InstallBattleForWindowsSubsystemForLinux201912

---

[mikutter 4.0.0](https://mikutter.hatenablog.com/entry/2019/12/25/001520)が 10 周年の節目で公開されめでたいので久しぶりに触ってみたところ、かつての[もぐの先生の手順](https://github.com/moguno/mikutter-windows)の頃とは段違いで導入しやすくなっていたので手順をまとめておく(2019/12/28 現在)。

---

# WSL(Ubuntu)をインストール

## ストアからインストールし、初期設定

```sh
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: y
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Installation successful!
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
```

## バージョンを確認

```sh
y@A:~$ cat /etc/os-release
```

> NAME="Ubuntu"
>
> VERSION="18.04.3 LTS (Bionic Beaver)"
>
> ID=ubuntu
>
> ID_LIKE=debian
>
> PRETTY_NAME="Ubuntu 18.04.3 LTS"
>
> VERSION_ID="18.04"
>
> HOME_URL="https://www.ubuntu.com/"
>
> SUPPORT_URL="https://help.ubuntu.com/"
>
> BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
>
> PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
>
> VERSION_CODENAME=bionic
>
> UBUNTU_CODENAME=bionic

## パッケージをアップデート

```sh
y@A:~$ sudo apt-get update && sudo apt upgrade -y
```

> The following packages will be upgraded:
>
> apport apt apt-utils base-files bash bind9-host bsdutils bzip2 cloud-init cpio curl dbus distro-info-data dmeventd dmsetup dnsutils dpkg e2fsprogs fdisk file friendly-recovery gcc-8-base git git-man grep initramfs-tools initramfs-tools-bin initramfs-tools-core iputils-ping iputils-tracepath landscape-common language-selector-common libapt-inst2.0 libapt-pkg5.0 libbind9-160 libblkid1 libbz2-1.0 libcom-err2 libcurl3-gnutls libcurl4 libdb5.3 libdbus-1-3 libdevmapper-event1.02.1 libdevmapper1.02.1 libdns-export1100 libdns1100 libdrm-common libdrm2 libelf1 libexpat1 libext2fs2 libfdisk1 libgcc1 libglib2.0-0 libglib2.0-data libgnutls30 libidn2-0 libirs160 libisc-export169 libisc169 libisccc160 libisccfg160 libldap-2.4-2 libldap-common liblvm2app2.2 liblvm2cmd2.02 liblwres160 libmagic-mgc libmagic1 libmount1 libmspack0 libnss-systemd libpam-systemd libpcap0.8 libprocps6 libpython3.6 libpython3.6-minimal libpython3.6-stdlib libseccomp2 libsmartcols1 libsqlite3-0 libss2 libssl1.1 libstdc++6 libsystemd0 libudev1 libuuid1 libxslt1.1 libzstd1 lvm2 mount netplan.io nplan open-vm-tools openssl patch procps python3-apport python3-cryptography python3-distupgrade python3-gdbm python3-jinja2 python3-problem-report python3-software-properties python3.6 python3.6-minimal snapd software-properties-common sosreport sudo systemd systemd-sysv tmux tzdata ubuntu-minimal ubuntu-release-upgrader-core ubuntu-server ubuntu-standard ubuntu-wsl udev unattended-upgrades update-notifier-common util-linux uuid-runtime vim vim-common vim-runtime vim-tiny wslu xkb-data xxd
>
> 131 upgraded, 56 newly installed, 0 to remove and 0 not upgraded.
>
> Need to get 82.6 MB of archives.
>
> After this operation, 232 MB of additional disk space will be used.

## 日本語環境を用意

```sh
y@A:~$ sudo apt-get install -y language-pack-ja
```

> The following NEW packages will be installed:
>
> language-pack-ja language-pack-ja-base
>
> 0 upgraded, 2 newly installed, 0 to remove and 0 not upgraded.
>
> Need to get 2591 kB of archives.
>
> After this operation, 12.0 MB of additional disk space will be used.

```sh
y@A:~$ sudo update-locale LANG=ja_JP.UTF-8
y@A:~$ sudo apt-get install -y gcc git libidn11-dev fonts-noto ttf-ancient-fonts uim uim-xim uim-anthy ruby ruby-dev
```

> The following NEW packages will be installed:
>
> adwaita-icon-theme anthy anthy-common at-spi2-core binutils binutils-common binutils-x86-64-linux-gnu build-essential cpp cpp-7 dconf-gsettings-backend dconf-service dpkg-dev fakeroot fontconfig fonts-ancient-scripts fonts-lato fonts-noto fonts-noto-cjk fonts-noto-hinted fonts-noto-mono fonts-noto-unhinted fonts-symbola g++ g++-7 gcc gcc-7 gcc-7-base glib-networking glib-networking-common glib-networking-services gsettings-desktop-schemas gtk-update-icon-cache hicolor-icon-theme humanity-icon-theme im-config javascript-common libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libanthy1 libanthyinput0 libasan4 libatk-bridge2.0-0 libatk1.0-0 libatk1.0-data libatomic1 libatspi2.0-0 libavahi-client3 libavahi-common-data libavahi-common3 libbinutils libc-dev-bin libc6-dev libcairo-gobject2 libcairo2 libcc1-0 libcilkrts5 libcolord2 libcroco3 libcups2 libdatrie1 libdconf1 libdouble-conversion1 libdpkg-perl libegl-mesa0 libegl1 libepoxy0 libevdev2 libfakeroot libfile-fcntllock-perl libgail-common libgail18 libgbm1 libgcc-7-dev libgcroots0 libgd3 libgdk-pixbuf2.0-0 libgdk-pixbuf2.0-bin libgdk-pixbuf2.0-common libgmp-dev libgmpxx4ldbl libgomp1 libgraphite2-3 libgtk-3-0 libgtk-3-bin libgtk-3-common libgtk2.0-0 libgtk2.0-bin libgtk2.0-common libgudev-1.0-0 libharfbuzz0b libidn11-dev libinput-bin libinput10 libisl19 libitm1 libjbig0 libjpeg-turbo8 libjpeg8 libjs-jquery libjson-glib-1.0-0 libjson-glib-1.0-common liblcms2-2 liblsan0 libm17n-0 libmpc3 libmpx2 libmtdev1 libotf0 libpango-1.0-0 libpangocairo-1.0-0 libpangoft2-1.0-0 libpixman-1-0 libproxy1v5 libqt5core5a libqt5dbus5 libqt5gui5 libqt5network5 libqt5svg5 libqt5widgets5 libqt5x11extras5 libquadmath0 librest-0.7-0 librsvg2-2 librsvg2-common libruby2.5 libsoup-gnome2.4-1 libsoup2.4-1 libstdc++-7-dev libthai-data libthai0 libtiff5 libtsan0 libubsan0 libuim-custom2 libuim-scm0 libuim8 libwacom-bin libwacom-common libwacom2 libwayland-client0 libwayland-cursor0 libwayland-egl1 libwayland-server0 libwebp6 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-randr0 libxcb-render-util0 libxcb-render0 libxcb-shm0 libxcb-util1 libxcb-xfixes0 libxcb-xinerama0 libxcb-xkb1 libxcursor1 libxkbcommon-x11-0 libxkbcommon0 linux-libc-dev m17n-db make manpages-dev pkg-config qt5-gtk-platformtheme qttranslations5-l10n rake ruby ruby-dev ruby-did-you-mean ruby-minitest ruby-net-telnet ruby-power-assert ruby-test-unit ruby2.5 ruby2.5-dev ruby2.5-doc rubygems-integration ttf-ancient-fonts ubuntu-mono uim uim-anthy uim-data uim-fep uim-gtk2.0 uim-gtk2.0-immodule uim-gtk3 uim-gtk3-immodule uim-plugins uim-qt5 uim-qt5-immodule uim-xim unzip wesperanto zip
>
> 0 upgraded, 196 newly installed, 0 to remove and 0 not upgraded.
>
> Need to get 167 MB of archives.
>
> After this operation, 549 MB of additional disk space will be used.

## GUI 環境を準備

### VcXsrv

```sh
y@A:~$ echo "export DISPLAY=localhost:0.0" >> ~/.bashrc
y@A:~$ source ~/.bashrc
```

[VcXsrv](https://sourceforge.net/projects/vcxsrv/) を Windows 上にインストールして起動(トレイに常駐)させ、WSL を再起動する

### ブラウザ

WSL から Windows 側のブラウザで指定した URL を開けるか確認する

```sh
y@A:~$ "/mnt/c/Program Files/Mozilla Firefox/firefox.exe" "http://example.net?a=1&b=2"
```

上記をシェルスクリプトにする

```sh
y@A:~$ nano work/firefoxwin
```

```sh
#!/bin/sh
"/mnt/c/Program Files/Mozilla Firefox/firefox.exe" "$1"
```

実行権限を付与

```sh
y@A:~$ chmod +x work/firefoxwin
```

# Mikutter をインストール

## Ruby ライブラリをインストール

```sh
y@A:~$ sudo gem install bundler
```

> 1 gem installed

```sh
y@A:~$ sudo gem install rake
```

> 1 gem installed

## Mikutter 本体をインストール

```sh
y@A:~$ cd ~/work
y@A:~/work$ git clone git://toshia.dip.jp/mikutter.git || git clone https://github.com/mikutter/mikutter.git
y@A:~/work$ cd ~/work/mikutter/
y@A:~/work/mikutter$ bundle install
```

> Bundle complete! 19 Gemfile dependencies, 41 gems now installed.

```sh
y@A:~/work$ mkdir -p ~/.mikutter/plugin; touch ~/.mikutter/plugin/display_requirements.rb; git clone https://github.com/toshia/twitter_api_keys.git ~/.mikutter/plugin/twitter_api_keys
```

コンシューマキー/シークレットを書き換え

```sh
y@A:~$ nano ~/.mikutter/plugin/twitter_api_keys/twitter_api_keys.rb
```

Mikutter を起動し、ブラウザ設定を変更(表示＞ URL を開く方法＞次のコマンドを使う に、作成したシェルスクリプトを指定)

```sh
y@A:~$ ruby ~/work/mikutter/mikutter.rb
```

# 日本語 IME・フォントをインストール

```sh
y@A:~\$ sudo apt install fcitx fcitx-mozc dbus-x11 x11-xserver-utils
```

> The following NEW packages will be installed:
>
> aspell aspell-en dictionaries-common emacsen-common enchant fcitx fcitx-bin fcitx-config-common fcitx-config-gtk fcitx-data fcitx-frontend-all fcitx-frontend-gtk2 fcitx-frontend-gtk3 fcitx-frontend-qt4 fcitx-frontend-qt5 fcitx-module-dbus fcitx-module-kimpanel fcitx-module-lua fcitx-module-x11 fcitx-modules fcitx-mozc fcitx-ui-classic gstreamer1.0-gl gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-pulseaudio gstreamer1.0-x hunspell-en-us libaa1 libaspell15 libaudio2 libavc1394-0 libbrotli1 libcaca0 libcdparanoia0 libdv4 libenchant1c2a libfcitx-config4 libfcitx-core0 libfcitx-gclient1 libfcitx-qt5-1 libfcitx-utils0 libgettextpo0 libgraphene-1.0-0 libgstreamer-gl1.0-0 libgstreamer-plugins-base1.0-0 libgstreamer-plugins-good1.0-0 libgstreamer1.0-0 libhunspell-1.6-0 libhyphen0 libiec61883-0 libjack-jackd2-0 libjavascriptcoregtk-4.0-18 liblua5.2-0 libmng2 libmp3lame0 libmpg123-0 libmysqlclient20 libnotify4 libopus0 liborc-0.4-0 libpresage-data libpresage1v5 libprotobuf10 libqt4-dbus libqt4-declarative libqt4-network libqt4-script libqt4-sql libqt4-sql-mysql libqt4-xml libqt4-xmlpatterns libqtcore4 libqtdbus4 libqtgui4 libraw1394-11 libsamplerate0 libsecret-1-0 libsecret-common libshout3 libspeex1 libtag1v5 libtag1v5-vanilla libtheora0 libtinyxml2.6.2v5 libtwolame0 libv4l-0 libv4lconvert0 libvisual-0.4-0 libvpx5 libwavpack1 libwebkit2gtk-4.0-37 libwebpdemux2 libwoff1 libxkbfile1 libzinnia0v5 mozc-data mozc-server mozc-utils-gui mysql-common notification-daemon presage qdbus qt-at-spi qtchooser qtcore4-l10n tegaki-zinnia-japanese x11-xserver-utils zenity zenity-common

```sh
y@A:~$ sudo sh -c "dbus-uuidgen > /var/lib/dbus/machine-id"
y@A:~$ sudo update-locale LANG=ja_JP.UTF8
y@A:~$ sudo apt install fonts-takao
```

> The following additional packages will be installed:
>
> fonts-takao-gothic fonts-takao-mincho fonts-takao-pgothic
>
> Suggested packages:
>
> fonts-takao fonts-takao-gothic fonts-takao-mincho fonts-takao-pgothic

WSL を再起動

```sh
y@A:~$exit
```

```sh
y@A:~$ export DISPLAY=:0.0
y@A:~$ export GTK_IM_MODULE=fcitx
y@A:~$ export XMODIFIERS=@im=fcitx
y@A:~$ export QT_IM_MODULE=fcitx
y@A:~$ export DefaultIMModule=fcitx
y@A:~$ xset -r 49
y@A:~$ fcitx-autostart
```

> # 以下は無視し、コマンドを再実行
>
> I/O warning : failed to load external entity "/usr/share/X11/xkb/rules/xorg.extras.xml"

```sh
y@A:~$ fcitx-autostart
```

> Fcitx is running correctly.

ホットキーを設定

```sh
y@A:~$ fcitx-config-gtk3
```

日本語入力できることを確認

```sh
y@A:~\$ ruby ~/work/mikutter/mikutter.rb
```

---

Copyright (c) 2019 YA-androidapp(https://github.com/YA-androidapp) All rights reserved.
