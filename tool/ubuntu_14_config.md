
## ubuntu basic configuration


### 1. Install basic
```
sudo apt-get install build-essential gcc make autoconf automake libtool gdb g++
cd /lib/modules/$(uname -r)/build/include/linux
sudo ln -s ../generated/utsrelease.h
sudo ln -s ../generated/autoconf.h
sudo ln -s ../generated/uapi/linux/version.h
```

### 2. vmvare tools
```
sudo ./vmware-install.pl
```

### 3. Download sougou-pinyin and config
```
fcitx-config-gtk3
```

