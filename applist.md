# Ubuntu 装机必备

## ubuntu应用

```shell
sudo apt-get install cmake
sudo apt-get install curl
sudo apt-get install libcurl4-openssl-dev
sudo apt-get install libssl-dev
sudo apt-get install openssl
sudo apt-get install libevent-dev
sudo apt-get install zlib1g-dev
sudo apt-get install natpmpc
sudo apt-get install natpmp-utils
sudo apt-get install natpmpc
sudo apt-get install qbittorrent
sudo apt-get install python3-pip
sudo apt-get install ipython
sudo apt-get install git
sudo apt-get install net-tools
```

## ubuntu用户登录界面背景修改

* 首先准备一张图片作为背景
* 将图片移动到/usr/share/backgrounds/目录下，并非必须
* 修改/etc/alternatives/gdm3.css
* 找到默认代码段并修改，建议提前备份，避免出错
* todo：脚本实现自动修改登录界面背景，因为每次系统升级登录界面背景都会被改回去

```css
#lockDialogGroup {
  background: #2c001e url(resource:///org/gnome/shell/theme/noise-texture.png);
  background-repeat: repeat; 
  }


#lockDialogGroup {
  background: #2c001e url(file:///usr/share/backgrounds/battlefields.jpg);
  background-repeat: no-repeat;
  background-size: 100% 100%;
  background-position: center;
}
```

保存后重启即可看到修改后的界面

## gnome美化

### 安装gnome-tweaks

```shell
sudo apt-get install gnome-tweaks
sudo apt-get install gnome-shell-extensions
```

安装完之后重启电脑，打开gnome-tweaks就可以看到更多的拓展程序了

### 主题、shell

将gnome主题下载并放入~/.themes文件夹中就可以在主题中看到已经下载的主题了，我使用了类mac主题Mojave

shell主题同主题一起，有了主题同样可以选择shell主题了，我这里还是使用Mojave

### 鼠标、图标

在~/.local/share/icons文件夹中放入鼠标、图标文件`alt+f2`之后就可以在gnome-tweaks中看到新加的图标和光标

鼠标我这里使用了默认的DMZ-Black

图标使用了McMojave-circle

### 安装dashtodock

通过`gnome-shell --version`确定要下载的版本

下载后运行`unzip -c ./openweather-extension@jenslody.de.v94.shell-extension.zip metadata.json`

其中，uuid即为安装包名字`dash-to-dock@micxgx.gmail.com`，将zip解压并将文件夹重命名为`dash-to-dock@micxgx.gmail.com`

然后将文件夹移动至extension目录下`mv dash-to-dock@micxgx.gmail.com ~/.local/share/gnome-extensions/`

最后`alt+f2`输入`r`重启gnome，再打开`gnome-tweaks`就可以看到`dash-to-dock`拓展了

### 安装albert

通过ppa安装albert

* `sudo add-apt-repository ppa:noobslab/macbuntu`
* `sudo apt-get udpate`
* `sudo apt-get install albert`

命令行输入albert开启albert，进入设置，hotkey设置为alt+e

进入gnome-tweaks开机启动设置，把albert设置为开机启动


## git配置

### git设置

```shell
git config --global user.email email
git config --global user.name name
git config --global https.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080
```

### git clone 速度太慢

解决办法：将github的dns解析增加到hosts文件中

```shell
$ nslookup github.com

Server:  127.0.0.53
Address: 127.0.0.53#53

Non-authoritative answer:
Name: github.com
Address: 52.74.223.119

$ nslookup http://ithub.global.ssl.fastly.net
Server: 127.0.0.53
Address: 127.0.0.53#53

Non-authoritative answer:
Name:	http://ithub.global.ssl.fastly.net
Address: 198.27.124.186
Name:	http://ithub.global.ssl.fastly.net
Address: 2001::1f0d:4b11

```

在 /etc/hosts最后增加一行

```shell
github.com    52.74.223.119
ithub.global.ssl.fastly.net    198.27.124.186

```

/etc/init.d/networking restart更新hosts文件

## 开发IDE

* pycharm for python
* vscode for common
* clion for c++
* atom for julia

## ubuntu 18.04 安装搜狗输入法

* 先在官网下载输入法deb版
* 在设置中增加中文并应用到整个系统,也可以删除英语语言,这样可以将输入法切换设置为super+space
* 注销后重新登录,切换汉语后,保持旧文件名称并不在提醒
* 到官网下载搜狗输入法linux版 `https://pinyin.sogou.com/linux/`
* 帮助页面: `https://pinyin.sogou.com/linux/help.php`

## 安装julia

### 安装

下载 `https://julialang.org/downloads/`

* `tar -xvf  julia-1.0.5-linux-x86_64.tar.gz`
* `mv julia-1.0.5 julia`
* `mv julia ~/app/`
* `cd ~/.local/bin/`
* `ln -s ~/app/julia/bin/julia julia`

### 安装后的一些设置

julia更换国内源，julia默认安装库是github，但是国内github不稳定，julia中文论坛给了设置国内镜像的方法

* 首先clone General`git clone --depth=1 git@github.com:JuliaRegistries/General.git`
* 将Genral移动到`mv General ~/.julia/registries/`
* 进入julia命令行

```julia
julia> using Pkg

julia> Pkg.add("PkgMirrors")
  Updating registry at `~/.julia/registries/General`
  Updating git-repo `git@github.com:JuliaRegistries/General.git`
 Resolving package versions...
 Installed PkgMirrors ─ v1.1.0
  Updating `~/.julia/environments/v1.0/Project.toml`
  [e0fc9d43] + PkgMirrors v1.1.0
  Updating `~/.julia/environments/v1.0/Manifest.toml`
  [e0fc9d43] + PkgMirrors v1.1.0
  [2a0f44e3] + Base64 
  [ade2ca70] + Dates 
  [8ba89e20] + Distributed 
  [b77e0a4c] + InteractiveUtils 
  [76f85450] + LibGit2 
  [8f399da3] + Libdl 
  [37e2e46d] + LinearAlgebra 
  [56ddb016] + Logging 
  [d6f4376e] + Markdown 
  [44cfe95a] + Pkg 
  [de0858da] + Printf 
  [3fa0cd96] + REPL 
  [9a3f8284] + Random 
  [ea8e919c] + SHA 
  [9e88b42a] + Serialization 
  [6462fe0b] + Sockets 
  [8dfed614] + Test 
  [cf7118a7] + UUIDs 
  [4ec0a83e] + Unicode 

julia> using PkgMirrors
[ Info: Precompiling PkgMirrors [e0fc9d43-7ff6-5671-9fff-748a5437251c]
julia> versioninfo()
Julia Version 1.0.5
Commit 3af96bcefc (2019-09-09 19:06 UTC)
Platform Info:
  OS: Linux (x86_64-pc-linux-gnu)
  CPU: AMD Ryzen 5 3600 6-Core Processor
  WORD_SIZE: 64
  LIBM: libopenlibm
  LLVM: libLLVM-6.0.0 (ORCJIT, znver1)
Environment:
  JULIA_PKG_SERVER = https://mirrors.ustc.edu.cn/julia

```

## amd3600安装tensorflow

### 安装tensorflow

* `sudo pip3 install keras`
* `sudo pip3 install h5py`
* `sudo pip3 install tensorflow`
* `sudo pip3 install pillow`
* `sudo pip3 install numpy`

### 测试tensorflow

```shell
$ python3
Python 3.6.9 (default, Jan 26 2021, 15:33:00) 
[GCC 8.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
/usr/local/lib/python3.6/dist-packages/tensorflow/python/framework/dtypes.py:516: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/usr/local/lib/python3.6/dist-packages/tensorflow/python/framework/dtypes.py:517: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/usr/local/lib/python3.6/dist-packages/tensorflow/python/framework/dtypes.py:518: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/usr/local/lib/python3.6/dist-packages/tensorflow/python/framework/dtypes.py:519: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/usr/local/lib/python3.6/dist-packages/tensorflow/python/framework/dtypes.py:520: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/usr/local/lib/python3.6/dist-packages/tensorflow/python/framework/dtypes.py:525: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
/usr/local/lib/python3.6/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:541: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/usr/local/lib/python3.6/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:542: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/usr/local/lib/python3.6/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:543: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/usr/local/lib/python3.6/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:544: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/usr/local/lib/python3.6/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:545: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/usr/local/lib/python3.6/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:550: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
>>> a =tf.constant(1)
>>> b =tf.constant(2)
>>> op = a+ b
>>> sess = tf.Session()
2021-06-05 19:03:11.631888: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2021-06-05 19:03:11.653737: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 3599990000 Hz
2021-06-05 19:03:11.654052: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x500bc60 executing computations on platform Host. Devices:
2021-06-05 19:03:11.654071: I tensorflow/compiler/xla/service/service.cc:175]   StreamExecutor device (0): <undefined>, <undefined>
>>> sess.run(op)
2021-06-05 19:03:37.203823: W tensorflow/compiler/jit/mark_for_compilation_pass.cc:1412] (One-time warning): Not using XLA:CPU for cluster because envvar TF_XLA_FLAGS=--tf_xla_cpu_global_jit was not set.  If you want XLA:CPU, either set that envvar, or use experimental_jit_scope to enable XLA:CPU.  To confirm that XLA is active, pass --vmodule=xla_compilation_cache=1 (as a proper command-line flag, not via TF_XLA_FLAGS) or set the envvar XLA_FLAGS=--xla_hlo_profile.
3
>>> sess.close()
```

在使用tensorflow的过程中发现了一个报警，`2021-06-05 19:03:11.631888: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA`，大概意思是：cpu支持avx扩展，但是目前安装的版本无法编译使用

在代码中加入

```python
import os
os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'
```

或者自己编译tensorflow也可以，这样不仅可以消除警告，tensorflow的性能也会得到提升

## 安装网易云音乐

* 从官网下载linux版网易云安装包: `https://music.163.com/#/download`
* sudo dpkg -i netease-cloud-music_1.2.1_amd64_ubuntu_20190428.deb
* 启动后报错: `Gtk-Message: 20:17:27.271: Failed to load module "canberra-gtk-module"` 重新安装一下canberra-gtk-module即可
* sudo apt-get install libcanberra-gtk-module

## ubuntu 动态壁纸（已弃用，壁纸太少且使用受限）

liveWallpaper是linux下的一个动态壁纸程序，与windows的wallpaperEngine功能相同

* `sudo add-pat-repository ppa:fyrmir/livewallpaper-daily`
* `sudo apt-get update`
* `sudo apt-get install livewallpaper`
* `sudo apt-get install livewallpaper-config livewallpaper-indicator`

### 设置livewallpaper开机启动

开机启动一般在/etc/rc.local或者/etc/rc.d/目录下，如果/etc/下含有多个rc目录，则可以使用命令`runlevel`查看当前系统运行的模式

```shell
$ runlevel 
N 5
```

可以看到当前系统运行在模式5下，因此，开机启动脚本在/etc/rc5.d目录中

在目录中使用命令ll，则可以看到，所有脚本都指向/etc/init.d中的脚本

```shell
/etc/rc5.d$ ll
总用量 16
drwxr-xr-x   2 root root  4096 5月  31 08:16 ./
drwxr-xr-x 128 root root 12288 6月   6 23:05 ../
lrwxrwxrwx   1 root root    15 5月  31 08:14 S01acpid -> ../init.d/acpid*
lrwxrwxrwx   1 root root    17 5月  31 08:14 S01anacron -> ../init.d/anacron*
lrwxrwxrwx   1 root root    16 5月  31 08:14 S01apport -> ../init.d/apport*
lrwxrwxrwx   1 root root    22 5月  31 08:14 S01avahi-daemon -> ../init.d/avahi-daemon*
lrwxrwxrwx   1 root root    19 5月  31 08:14 S01bluetooth -> ../init.d/bluetooth*
lrwxrwxrwx   1 root root    26 5月  31 08:14 S01console-setup.sh -> ../init.d/console-setup.sh*
lrwxrwxrwx   1 root root    14 5月  31 08:14 S01cron -> ../init.d/cron*
lrwxrwxrwx   1 root root    14 5月  31 08:14 S01cups -> ../init.d/cups*
lrwxrwxrwx   1 root root    22 5月  31 08:14 S01cups-browsed -> ../init.d/cups-browsed*
lrwxrwxrwx   1 root root    14 5月  31 08:14 S01dbus -> ../init.d/dbus*
lrwxrwxrwx   1 root root    14 5月  31 08:14 S01gdm3 -> ../init.d/gdm3*
lrwxrwxrwx   1 root root    21 5月  31 08:14 S01grub-common -> ../init.d/grub-common*
lrwxrwxrwx   1 root root    20 5月  31 08:14 S01irqbalance -> ../init.d/irqbalance*
lrwxrwxrwx   1 root root    20 5月  31 08:14 S01kerneloops -> ../init.d/kerneloops*
lrwxrwxrwx   1 root root    18 5月  31 08:14 S01plymouth -> ../init.d/plymouth*
lrwxrwxrwx   1 root root    15 5月  31 08:14 S01rsync -> ../init.d/rsync*
lrwxrwxrwx   1 root root    17 5月  31 08:14 S01rsyslog -> ../init.d/rsyslog*
lrwxrwxrwx   1 root root    15 5月  31 08:14 S01saned -> ../init.d/saned*
lrwxrwxrwx   1 root root    27 5月  31 08:14 S01speech-dispatcher -> ../init.d/speech-dispatcher*
lrwxrwxrwx   1 root root    23 5月  31 08:14 S01spice-vdagent -> ../init.d/spice-vdagent*
lrwxrwxrwx   1 root root    29 5月  31 08:14 S01unattended-upgrades -> ../init.d/unattended-upgrades*
lrwxrwxrwx   1 root root    15 5月  31 08:14 S01uuidd -> ../init.d/uuidd*
lrwxrwxrwx   1 root root    18 5月  31 08:14 S01whoopsie -> ../init.d/whoopsie*
```

这些也正是我们默认开机状态下，要启动的服务，因此我们需要将我们的脚本放在/etc/init.d目录下同时在/etc/rc5.d中创建软链接，就可以做到开机启动了。

```shell
which livewallpaper
sudo ln -s /usr/bin/livewallpaper livewallpaper
sudo ln -s ../init.d/livewallpaper livewallpaper
```

## v2ray安装

使用一键安装命令`bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)`这条命令会安装以下文件

```js
installed: /usr/local/bin/v2ray
installed: /usr/local/bin/v2ctl
installed: /usr/local/share/v2ray/geoip.dat
installed: /usr/local/share/v2ray/geosite.dat
installed: /usr/local/etc/v2ray/config.json
installed: /var/log/v2ray/
installed: /var/log/v2ray/access.log
installed: /var/log/v2ray/error.log
installed: /etc/systemd/system/v2ray.service
installed: /etc/systemd/system/v2ray@.service
```

配置v2ray脚本`/usr/local/etc/v2ray/config.json`，也可以自己下载v2ray core，解压之后编辑文件vpoint_vmess_socks.json

其中`inbounds`段为服务端配置段，`outbounds`为客户端配置段，根据服务端配置修改客户端配置文件，其中protocol为`vmess`，adress和port修改为服务端地址和端口，id与服务端配置的id保持一致

```json
{
  "log": {
    "access": "/var/log/v2ray/access.log",
    "error": "/var/log/v2ray/error.log",
    "loglevel": "warning"
  },
  "inbounds": [{
    "port": 1080,
    "listen": "127.0.0.1",
    "protocol": "socks",
    "settings": {
      "auth": "noauth",
      "udp": false,
      "ip": "127.0.0.1"
    }
  }],
  "outbounds": [{
    "protocol": "vmess",
    "settings": {
        "vnext":[
 {
     "address":"******",
     "port":443,
     "users":[
     {
      "id":"********",
     }
     ]
 }
 ]
    },
    "tag": "direct"
  }],
  "policy": {
    "levels": {
      "0": {"uplinkOnly": 0}
    }
  }
}
```

### 设置全局代理（服务端暂时被封，没有测试以下内容）

```shell
export http_proxy="http://127.0.0.1:1080"
export https_proxy="https://127.0.0.1:1080"
```

`wget https://www.google.com`测试代理是否成功

出现错误：`2021/06/11 23:06:52 tcp:127.0.0.1:39470 rejected  v2ray.com/core/proxy/socks: unknown Socks version: 67`

可能原因：开启的是socks代理，但是浏览器中配置了http代理

解决方法：在v2ray中配置一个http入站代理，再把浏览器的设置指向这个代理

### 开机启动v2ray

```shell
sudo ln -s ~/app/v2ray/v2ray /etc/init.d/v2ray
sudo ln -s /etc/init.d/v2ray /etc/rc5.d/v2ray
```

`systemctl enable v2ray`出现错误`update-rc.d: error: no runlevel symlinks to modify, aborting!`

解决办法：sudo update-rc.d v2ray defaults
