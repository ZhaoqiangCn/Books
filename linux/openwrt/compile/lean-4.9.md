# Lean-4.9

### 安装依赖

```bash
sudo apt-get update
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx autoconf automake libtool autopoint
```

### 克隆lean的包到本地

```text
git clone https://github.com/ZhaoqiangCn/lede
```

### 安装feeds

```text
./scripts/feeds update -a && ./scripts/feeds install -a
```

### 进行编译

注意dsnmasq 和 dnsmasq-full 只能选一个

```bash
make menuconfig
```

### 进行编译，输入下列命令

```text
make -j4 V=s
```



