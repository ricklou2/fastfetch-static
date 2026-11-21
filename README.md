# fastfetch — Fully Static Build

**Languages:** [English](#english) | [简体中文](#简体中文) | [繁體中文](#繁體中文)

---

## English

A standalone, fully static build of **fastfetch**, a system information and hardware detection tool, for four Linux architectures, bundled with the upstream source code. The executables have no dynamic interpreter and no shared-library dependencies, so they run directly on Android phones, embedded devices, and minimal Linux systems.

### Executables

| File | Size | MD5 |
|---|---:|---|
| fastfetch-linux-arm64 | 1,554,104 B | `0288b6c4ac7fc8c98241610f19ef4d51` |
| fastfetch-linux-armhf | 1,572,944 B | `1641be774df7964409c92af54ae90272` |
| fastfetch-linux-x64 | 1,669,592 B | `edc86f07a7778740cec0690ebf0cc936` |
| fastfetch-linux-x86 | 1,542,380 B | `95110b456f5be03b29f667c70bbd6ca4` |

### Static verification

```bash
llvm-readelf -l <binary> | grep -c INTERP   # 0
llvm-readelf -d <binary> | grep -c NEEDED   # 0
llvm-readelf -l <binary> | awk '/LOAD/{print $NF}' | sort -u   # 0x4000
```

All binaries report `INTERP=0`, `NEEDED=0`, and `LOAD align=0x4000` — musl static executables.

### Install and run

```bash
# Linux
install -m755 fastfetch-linux-x64 /usr/local/bin/fastfetch
fastfetch --help

# Android (via adb)
adb push fastfetch-linux-arm64 /data/local/tmp/fastfetch
adb shell "chmod 755 /data/local/tmp/fastfetch"
adb shell "/data/local/tmp/fastfetch --help"
```

### Repository layout

```
bins/   Executables for linux-x64/x86/arm64/armhf
src/    Upstream source: fastfetch-2.57.1.tar.gz
```

### Offline build

The source is included under `src/` for fully offline reproduction, using the zig toolchain (musl cross-compilation):

```bash
tar xf <source archive> && cd <source dir>
CC="zig cc -target x86_64-linux-musl -static" ./configure --host=x86_64-linux-musl --disable-shared --enable-static
make -j4
```

Architecture triples:

| Target | Linux triple |
|---|---|
| x64 | x86_64-linux-musl |
| x86 | x86-linux-musl |
| arm64 | aarch64-linux-musl |
| armhf | arm-linux-musleabihf |

### Known limitations

- A small number of sub-features that rely on host tools may be unavailable on very restricted systems.

---

## 简体中文

**fastfetch** 的独立全静态构建包，系统信息与硬件检测工具，覆盖四个 Linux 架构，并附上游源码。可执行文件无动态解释器、无共享库依赖，可直接在安卓手机、嵌入式设备和精简 Linux 系统上运行。

### 可执行文件

| 文件 | 体积 | MD5 |
|---|---:|---|
| fastfetch-linux-arm64 | 1,554,104 B | `0288b6c4ac7fc8c98241610f19ef4d51` |
| fastfetch-linux-armhf | 1,572,944 B | `1641be774df7964409c92af54ae90272` |
| fastfetch-linux-x64 | 1,669,592 B | `edc86f07a7778740cec0690ebf0cc936` |
| fastfetch-linux-x86 | 1,542,380 B | `95110b456f5be03b29f667c70bbd6ca4` |

### 静态性核验

```bash
llvm-readelf -l <二进制> | grep -c INTERP   # 0
llvm-readelf -d <二进制> | grep -c NEEDED   # 0
llvm-readelf -l <二进制> | awk '/LOAD/{print $NF}' | sort -u   # 0x4000
```

全部为 `INTERP=0`、`NEEDED=0`、`LOAD align=0x4000`：musl 静态可执行文件。

### 安装与运行

```bash
# Linux
install -m755 fastfetch-linux-x64 /usr/local/bin/fastfetch
fastfetch --help

# Android（通过 adb）
adb push fastfetch-linux-arm64 /data/local/tmp/fastfetch
adb shell "chmod 755 /data/local/tmp/fastfetch"
adb shell "/data/local/tmp/fastfetch --help"
```

### 仓库结构

```
bins/   四个可执行文件（linux-x64/x86/arm64/armhf）
src/    上游源码：fastfetch-2.57.1.tar.gz
```

### 离线编译

源码位于 `src/`，可完全离线复现，工具链使用 zig（musl 交叉编译）：

```bash
tar xf <源码包> && cd <源码目录>
CC="zig cc -target x86_64-linux-musl -static" ./configure --host=x86_64-linux-musl --disable-shared --enable-static
make -j4
```

架构 triple：

| 目标 | Linux triple |
|---|---|
| x64 | x86_64-linux-musl |
| x86 | x86-linux-musl |
| arm64 | aarch64-linux-musl |
| armhf | arm-linux-musleabihf |

### 已知限制

- 在受限严重的系统上，个别依赖宿主工具的子功能可能不可用。

---

## 繁體中文

**fastfetch** 的獨立全靜態建構包，系統資訊與硬體偵測工具，涵蓋四個 Linux 架構，並附上游原始碼。可執行檔無動態直譯器、無共用程式庫相依性，可直接在安卓手機、嵌入式裝置和精簡 Linux 系統上執行。

### 可執行檔

| 檔案 | 體積 | MD5 |
|---|---:|---|
| fastfetch-linux-arm64 | 1,554,104 B | `0288b6c4ac7fc8c98241610f19ef4d51` |
| fastfetch-linux-armhf | 1,572,944 B | `1641be774df7964409c92af54ae90272` |
| fastfetch-linux-x64 | 1,669,592 B | `edc86f07a7778740cec0690ebf0cc936` |
| fastfetch-linux-x86 | 1,542,380 B | `95110b456f5be03b29f667c70bbd6ca4` |

### 靜態性核驗

```bash
llvm-readelf -l <可執行檔> | grep -c INTERP   # 0
llvm-readelf -d <可執行檔> | grep -c NEEDED   # 0
llvm-readelf -l <可執行檔> | awk '/LOAD/{print $NF}' | sort -u   # 0x4000
```

全部為 `INTERP=0`、`NEEDED=0`、`LOAD align=0x4000`：musl 靜態可執行檔。

### 安裝與執行

```bash
# Linux
install -m755 fastfetch-linux-x64 /usr/local/bin/fastfetch
fastfetch --help

# Android（透過 adb）
adb push fastfetch-linux-arm64 /data/local/tmp/fastfetch
adb shell "chmod 755 /data/local/tmp/fastfetch"
adb shell "/data/local/tmp/fastfetch --help"
```

### 倉庫結構

```
bins/   四個可執行檔（linux-x64/x86/arm64/armhf）
src/    上游原始碼：fastfetch-2.57.1.tar.gz
```

### 離線建構

原始碼位於 `src/`，可完全離線重現，工具鏈使用 zig（musl 交叉編譯）：

```bash
tar xf <原始碼封存> && cd <原始碼目錄>
CC="zig cc -target x86_64-linux-musl -static" ./configure --host=x86_64-linux-musl --disable-shared --enable-static
make -j4
```

架構 triple：

| 目標 | Linux triple |
|---|---|
| x64 | x86_64-linux-musl |
| x86 | x86-linux-musl |
| arm64 | aarch64-linux-musl |
| armhf | arm-linux-musleabihf |

### 已知限制

- 在受限嚴重的系統上，個別依賴宿主工具的子功能可能無法使用。
