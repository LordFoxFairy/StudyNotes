# Yew 篇

## 环境配置

### 创建项目 

建一个二进制项目

```bash
cargo new --bin yew-app && cd yew-app
```

### 添加依赖

添加 yew 到依赖库中（这里 可以查看最新版本的 Yew）

```toml
[package]
name = "yew-app"
version = "0.1.0"
edition = "2021"

[dependencies]
yew = { git = "https://github.com/yewstack/yew/", features = ["csr"] }
```

- 如果正在构建应用程序，则只需要 csr 功能。它将启用 Renderer 和所有与客户端渲染相关的代码。

- 如果正在制作一个库，请不要启用此功能，因为它会将客户端渲染逻辑拉入服务器端渲染包。

### 安装trunk

```bash
cargo install trunk
```

> 可能需要如下帮助。

#### Windows安装

- 下载 vcpkg 【选一个】

```bash
git clone https://gitee.com/mirrors/vcpkg.git
git clone https://gitee.com/SpikeXue_admin/vcpkg.git
git clone https://gitee.com/Link-Not-Found/vcpkg.git
```

- 修改vcpkg-tool的下载地址

在`scripts文件夹`下找到`bootstrap.ps1`、`bootstrap.sh`和`update-vcpkg-tool-metadata.ps1`文件。

1) 在windows环境下，实际执行的脚本是boostrap.ps1，具体代码为：

```bash
# 将原来的代码注释掉
# if ($env:PROCESSOR_ARCHITECTURE -eq 'ARM64' -or $env:PROCESSOR_IDENTIFIER -match "ARMv[8,9] \(64-bit\)") {
#     & "$scriptsDir/tls12-download-arm64.exe" "mirror.ghproxy.com/https://github.com" "/microsoft/vcpkg-tool/releases/download/$versionDate/vcpkg-arm64.exe" "$vcpkgRootDir\vcpkg.exe"
# } else {
#     & "$scriptsDir/tls12-download.exe" "mirror.ghproxy.com/https://github.com" "/microsoft/vcpkg-tool/releases/download/$versionDate/vcpkg.exe" "$vcpkgRootDir\vcpkg.exe"
# }

# Write-Host ""

# if ($LASTEXITCODE -ne 0)
# {
#     Write-Error "Downloading vcpkg.exe failed. Please check your internet connection, or consider downloading a recent vcpkg.exe from https://github.com/microsoft/vcpkg-tool with a browser."
#     throw
# }

# Write-Host ""

# 检测处理器架构  
if ($env:PROCESSOR_ARCHITECTURE -eq 'ARM64' -or $env:PROCESSOR_IDENTIFIER -match "ARMv[8,9] \(64-bit\)") {  
    $url = "https://mirror.ghproxy.com/https://github.com/microsoft/vcpkg-tool/releases/download/$versionDate/vcpkg-arm64.exe"  
    $outputFile = "$vcpkgRootDir\vcpkg.exe"  
} else {  
    $url = "https://mirror.ghproxy.com/https://github.com/microsoft/vcpkg-tool/releases/download/$versionDate/vcpkg.exe"  
    $outputFile = "$vcpkgRootDir\vcpkg.exe"  
}  
try{
    # 使用BITS启动文件传输  
    Start-BitsTransfer -Souce $url -Destination $outputFile -ErrorAction Stop 
    Write-Host ""
}
catch {
    Write-Error "Downloading vcpkg.exe failed. Please check your internet connection, or consider downloading a recent vcpkg.exe from https://github.com/microsoft/vcpkg-tool with a browser."
    throw
}
```

2. 修改第三方库的下载地址：在scripts/cmake文件夹下，找到`vcpkg_download_distfile`函数，在`vcpkg_list(SET urls_param)`后修改：

```bash
    vcpkg_list(SET urls_param)
    # 新增一个变量，存储修改后的url集合，用于在控制台中打印
    vcpkg_list(SET arg_URLS_Real)
    foreach(url IN LISTS arg_URLS)
        # 将第三方库的地址更换为国内镜像源地址，这五个只是我目前找到的，如果有更多的需要替换的地址，形如：
        # string(REPLACE <oldUrl> <newUrl> url "${url}")，按照这个格式继续添加即可
        string(REPLACE "http://download.savannah.nongnu.org/releases/gta/" "https://marlam.de/gta/releases/" url "${url}")
		string(REPLACE "https://github.com/" "https://mirror.ghproxy.com/https://github.com/" url "${url}")
		string(REPLACE "https://ftp.gnu.org/" "https://mirrors.aliyun.com/" url "${url}")
		string(REPLACE "https://raw.githubusercontent.com/" "https://mirror.ghproxy.com/https://raw.githubusercontent.com/" url "${url}")
		string(REPLACE "http://ftp.gnu.org/pub/gnu/" "https://mirrors.aliyun.com/gnu/" url "${url}")
		string(REPLACE "https://ftp.postgresql.org/pub/" "https://mirrors.tuna.tsinghua.edu.cn/postgresql/" url "${url}")
		string(REPLACE "https://support.hdfgroup.org/ftp/lib-external/szip/2.1.1/src/" "https://distfiles.macports.org/szip/" url "${url}")

        vcpkg_list(APPEND urls_param "--url=${url}")
        # 存储新的第三方库下载地址
        vcpkg_list(APPEND arg_URLS_Real "${url}")
    endforeach()
    if(NOT vcpkg_download_distfile_QUIET)
        # message(STATUS "Downloading ${arg_URLS} -> ${arg_FILENAME}...")
        # 控制台打印信息时，使用实际的下载地址，因为arg_URLS变量无法修改(我不会改，好像是改不了)
        message(STATUS "Downloading ${arg_URLS_Real} -> ${arg_FILENAME}...")
    endif()
```

- 生成vcpkg.exe

```bash
.\vcpkg\bootstrap-vcpkg.bat
```

- 使用 vcpkg 安装 openssl

```bash
.\vcpkg\vcpkg install openssl:x64-windows
```

> 注意这里下载超时，可以观察要下载的文件，提前下载到 .\vcpkg\downloads 目录下即可。
>
> 注意下载后的重命名。

- 配置环境变量

```bash
X86_64_PC_WINDOWS_MSVC_OPENSSL_LIB_DIR =  D:\Program Files\vcpkg\packages\openssl_x64-windows\lib
X86_64_PC_WINDOWS_MSVC_OPENSSL_INCLUDE_DIR = D:\Program Files\vcpkg\packages\openssl_x64-windows\include
X86_64_PC_WINDOWS_MSVC_OPENSSL_DIR = D:\Program Files\vcpkg\packages\openssl_x64-windows
```

- 重新安装

```bash
cargo install trunk
```



#### 其他安装

##### linux下安装 vcpkg

同【修改vcpkg-tool的下载地址】步骤

```bash
sed -i 's#https://github.com/#https://mirror.ghproxy.com/https://github.com/#g' /app/vcpkg/scripts/bootstrap.sh \
    && sed -i 's#https://github.com/#https://mirror.ghproxy.com/https://github.com/#g' /app/vcpkg/scripts/vcpkgTools.xml \
    && sed -z -i 's|    vcpkg_list(SET urls_param)\n    foreach(url IN LISTS arg_URLS)\n        vcpkg_list(APPEND urls_param "--url=${url}")\n    endforeach()\n    if(NOT vcpkg_download_distfile_QUIET)\n        message(STATUS "Downloading ${arg_URLS} -> ${arg_FILENAME}...")\n    endif()|    vcpkg_list(SET urls_param)\n    vcpkg_list(SET arg_URLS_Real)\n    foreach(url IN LISTS arg_URLS)\n        string(REPLACE "http://download.savannah.nongnu.org/releases/gta/" "https://marlam.de/gta/releases/" url "${url}")\n        string(REPLACE "https://github.com/" "https://mirror.ghproxy.com/https://github.com/" url "${url}")\n        string(REPLACE "https://ftp.gnu.org/" "https://mirrors.aliyun.com/" url "${url}")\n        string(REPLACE "https://raw.githubusercontent.com/" "https://mirror.ghproxy.com/https://raw.githubusercontent.com/" url "${url}")\n        string(REPLACE "http://ftp.gnu.org/pub/gnu/" "https://mirrors.aliyun.com/gnu/" url "${url}")\n        string(REPLACE "https://ftp.postgresql.org/pub/" "https://mirrors.tuna.tsinghua.edu.cn/postgresql/" url "${url}")\n        string(REPLACE "https://support.hdfgroup.org/ftp/lib-external/szip/2.1.1/src/" "https://distfiles.macports.org/szip/" url "${url}")\n        vcpkg_list(APPEND urls_param "--url=${url}")\n        vcpkg_list(APPEND arg_URLS_Real "${url}")\n    endforeach()\n    if(NOT vcpkg_download_distfile_QUIET)\n        message(STATUS "Downloading ${arg_URLS_Real} -> ${arg_FILENAME}...")\n    endif()|g' /app/vcpkg/scripts/cmake/vcpkg_download_distfile.cmake
```

## 第一个静态页面

将下面代码复制到代码main.rs中。

```rust
use yew::prelude::*;

#[function_component(App)]
fn app() -> Html {
    html! {
        <h1>{ "Hello World" }</h1>
    }
}

fn main() {
    yew::Renderer::<App>::new().render();
}
```

现在，在项目的根目录创建一个 index.html。

```html
<!doctype html>
<html lang="en">
    <head></head>
    <body></body>
</html>
```

接下里，启动开发服务器。运行以下命令以在本地构建并提供应用程序。

```bash
trunk serve --open
```

> 删除选项 '--open' 以不打开默认浏览器 trunk serve。

Trunk 将在的默认浏览器中打开你的应用程序，监视项目目录，并在修改任何源文件时帮助重建应用程序。如果套接字被另一个应用程序使用，这将失败。默认情况下，服务器将在地址 '127.0.0.1' 和端口 '8080' 上侦听 => http://localhost:8080。要更改它，请创建以下文件并根据需要进行编辑`Trunk.toml`。

```bash
[serve]
# The address to serve on LAN.
address = "127.0.0.1"
# The address to serve on WAN.
# address = "0.0.0.0"
# The port to serve on.
port = 8000
```

可以运行 `trunk help` 和 `trunk help <subcommand>` 以获取有关正在发生的事情的更多详细信息。

### 构建 HTML

