# foo_scrobble (汉化版)

## 概述

foo_scrobble 是一个 foobar2000 的插件，用于向 [https://www.last.fm/](https://www.last.fm/) 提交音乐的播放记录。

- 使用 [Scrobbling 2.0 API](https://www.last.fm/api/scrobbling)。您可以在 last.fm 上授予插件访问权限，无需在 foobar2000 中输入账号和密码。
- 支持设置 “正在播放” 通知状态。
- 能够良好的处理间歇性的网络中断或重连问题。不会出现 “等待连接” 的情况。
- 自动管理待提交的播放记录缓存，无需手动提交。
- 允许为提交的播放记录设置自定义标签。

使用前，请打开 foobar2000 的参数选项页面，导航至 `工具 > Last.fm`，然后使用顶部的按钮授权您的客户端。悬浮在按钮上时会有详细的操作说明。


## 依赖

您可能需要安装 [Visual C++ Redistributable for Visual Studio 2015-2022](https://aka.ms/vs/17/release/vc_redist.x86.exe)。
对于 Windows 7 的用户还需要安装 [Windows 7 更新 (KB2999226)](https://www.microsoft.com/en-us/download/details.aspx?id=49077)，
通常 Windows Update 已自动安装。


## 编译

需要 Visual Studio 2022 (17.3.0) 并额外安装以下内容：
- Workloads:
  - Desktop development with C++
  - .NET desktop development
  - .NET Core cross-platform development
- Components:
  - MSVC v143 - VS 2022 C++ x64/x86 build tools (v14.33-17.3)

.NET workloads 对于编译 `foo_scrobble` 而言不是必需的，
但包含的测试服务器项目需要用到，
并且 `build.proj` 文件将假设已经安装 .NET workloads。

需要依赖使用 `foo_scrobble-deps` NuGet 包。 因此在打开解决方案或从命令行构建之前，
请先运行 `eng\Build-Dependencies.ps1` 脚本来构建并安装该包到解决方案中。foobar2000 SDK 已经包含在该仓库内。

在 Visual Studio Developer 命令提示符中运行以下命令以构建发行版本：
```
msbuild -m build.proj
```
将会在 `build\publish` 目录中创建 `foo_scrobble-<VERSION>.fb2k-component` 和 `foo_scrobble-<VERSION>.zip` 压缩文件(包含 DLL 和符号文件)。

## 开源协议

使用 [MIT License](LICENSE.txt) 授权.
