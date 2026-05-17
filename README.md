# 千月堂·CLI (QianYueTang.CLI)

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Framework](https://img.shields.io/badge/.NET%2010-windows-brightgreen)
![Platform](https://img.shields.io/badge/platform-Windows%2010+-purple)

一款基于 WPF 开发的现代化网络设备管理与终端仿真工具，集成了 LLDP 协议分析、SSH 连接、数据包捕获等专业功能。

## 📋 目录

- [项目简介](#项目简介)
- [核心功能](#核心功能)
- [技术栈](#技术栈)
- [系统要求](#系统要求)
- [快速开始](#快速开始)
- [项目结构](#项目结构)
- [从源码构建](#从源码构建)
- [使用指南](#使用指南)
- [配置说明](#配置说明)
- [常见问题](#常见问题)
- [贡献指南](#贡献指南)
- [开源协议](#开源协议)

---

## 项目简介

**千月堂·CLI** 是一款面向网络工程师和系统集成人员的桌面应用程序，提供统一的界面来管理网络设备、执行 SSH 连接、捕获和分析网络数据包。

### 🎯 设计理念

- **Material Design 风格**：采用 Google Material Design 设计规范，界面简洁美观
- **MVVM 架构**：清晰的代码分层，易于维护和扩展
- **模块化设计**：功能模块独立，支持按需加载
- **响应式布局**：支持窗口缩放和自适应布局

---

## 核心功能

### 🌐 网络设备管理
- **设备发现**：自动发现局域网内的网络设备
- **LLDP 协议支持**：解析 LLDP 数据包，获取邻居设备信息
- **设备分组**：按设备类型、厂商等维度自动分组
- **状态监控**：实时显示设备连接状态

### 🖥️ 终端仿真
- **SSH 连接**：基于 SSH.NET 实现安全的远程连接
- **多会话管理**：同时管理多个 SSH 会话
- **终端仿真**：支持 VT100、xterm 等终端类型
- **串口通信**：支持通过串口连接设备

### 📡 数据包捕获
- **实时捕获**：基于 SharpPcap 实现网络数据包捕获
- **协议分析**：解析以太网、IP、TCP、UDP 等协议
- **过滤器**：支持 BPF (Berkeley Packet Filter) 语法
- **数据包导出**：将捕获的数据包保存为 PCAP 格式

### 🗃️ 数据管理
- **SQLite 数据库**：使用 Entity Framework Core + SQLite 存储配置和历史数据
- **配置管理**：保存连接配置、设备信息等
- **日志记录**：记录操作日志和异常信息

---

## 技术栈

### 核心框架
| 技术 | 版本 | 用途 |
|------|------|------|
| .NET 10 SDK | 10.0.300+ | 应用程序框架 |
| WPF (Windows Presentation Foundation) | - | UI 框架 |
| CommunityToolkit.Mvvm | 8.4.2 | MVVM 框架 |

### UI 组件
| 技术 | 版本 | 用途 |
|------|------|------|
| MaterialDesignThemes | 5.3.1 | Material Design 风格控件 |
| MaterialDesignInXAML | 5.3.1 | XAML 资源字典 |

### 网络与通信
| 技术 | 版本 | 用途 |
|------|------|------|
| SSH.NET | 2025.1.0 | SSH 客户端实现 |
| SharpPcap | 6.3.1 | 数据包捕获 |
| PacketDotNet | 1.4.8 | 数据包解析 |
| FxSocket.Emulation | 5.0.1242 | 终端仿真 |

### 数据与配置
| 技术 | 版本 | 用途 |
|------|------|------|
| Microsoft.EntityFrameworkCore.Sqlite | 10.0.7 | ORM + 数据库 |
| Microsoft.Extensions.Configuration | 10.0.7 | 配置管理 |
| Newtonsoft.Json | 13.0.4 | JSON 处理 |

### Web 集成
| 技术 | 版本 | 用途 |
|------|------|------|
| Microsoft.Web.WebView2 | 1.0.3912.50 | 嵌入式浏览器 |

---

## 系统要求

### 最低配置
- **操作系统**：Windows 10 版本 1809 或更高版本
- **CPU**：1 GHz 或更快的处理器
- **内存**：4 GB RAM
- **硬盘**：500 MB 可用空间
- **.NET Runtime**：.NET 10 Desktop Runtime

### 推荐配置
- **操作系统**：Windows 11
- **CPU**：多核 2 GHz 或更快
- **内存**：8 GB RAM 或更多
- **硬盘**：1 GB 可用空间（SSD 推荐）
- **网卡**：支持混杂模式的以太网适配器（用于数据包捕获）

---

## 快速开始

### 1. 下载发布版本

前往 [Releases](https://github.com/你的用户名/QianYueTang.CLI/releases) 页面下载最新版本的安装包。

### 2. 安装

#### 方式一：安装包（推荐）
1. 双击 `QianYueTang.CLI.Setup.exe`
2. 按照安装向导完成安装
3. 从开始菜单启动应用程序

#### 方式二：便携版
1. 解压 `QianYueTang.CLI.Portable.zip` 到任意文件夹
2. 双击 `QianYueTang.CLI.exe` 启动

### 3. 首次运行

首次运行时会自动创建配置文件 (`appsettings.json`) 和 SQLite 数据库。

---

## 项目结构

```
QianYueTang.CLI/
├── Core/                          # 核心业务逻辑层
│   ├── Models/                    # 领域模型
│   │   ├── Device.cs              # 设备模型
│   │   ├── ConnectionConfig.cs    # 连接配置
│   │   └── PacketRecord.cs       # 数据包记录
│   ├── Services/                 # 业务服务
│   │   ├── DeviceDiscoveryService.cs
│   │   ├── LldpAnalysisService.cs
│   │   └── PacketCaptureService.cs
│   └── Interfaces/               # 接口定义
│       ├── IDeviceService.cs
│       └── IPacketCaptureService.cs
│
├── Infrastructure/                # 基础设施层
│   ├── Data/                     # 数据访问
│   │   ├── AppDbContext.cs        # EF Core 上下文
│   │   └── Migrations/           # 数据库迁移
│   ├── Repositories/             # 仓储模式实现
│   │   ├── DeviceRepository.cs
│   │   └── ConfigRepository.cs
│   └── External/                 # 外部服务集成
│       └── MacVendorLookup.cs
│
├── Presentation/                 # 表示层 (WPF)
│   ├── Views/                    # XAML 视图
│   │   ├── Home/
│   │   │   └── WelcomePage.xaml
│   │   ├── Device/
│   │   │   ├── DeviceListView.xaml
│   │   │   └── DevicePanel.xaml
│   │   ├── Terminal/
│   │   │   └── TerminalPage.xaml
│   │   └── Settings/
│   │       └── SettingsPage.xaml
│   ├── ViewModels/               # ViewModel
│   │   ├── MainViewModel.cs
│   │   ├── DeviceListViewModel.cs
│   │   ├── ScanViewModel.cs
│   │   └── LoginViewModel.cs
│   ├── Converters/               # 值转换器
│   │   ├── BoolToBrushConverter.cs
│   │   ├── BoolToVisibilityConverter.cs
│   │   └── ...
│   ├── Styles/                   # XAML 资源字典
│   │   ├── ColorResources.xaml
│   │   ├── LayoutResources.xaml
│   │   ├── TypographyResources.xaml
│   │   └── AnimationResources.xaml
│   ├── Behaviors/                # 交互行为
│   └── Controls/                 # 自定义控件
│
├── App.xaml                      # 应用程序入口 (XAML)
├── App.xaml.cs                   # 应用程序入口 (代码后台)
├── MainWindow.xaml               # 主窗口
└── MainWindow.xaml.cs
```

### 架构说明

采用 **分层架构 + MVVM 模式**：

```
┌─────────────────────────────────────┐
│         Presentation Layer          │  ← Views, ViewModels, Styles
├─────────────────────────────────────┤
│           Core Layer                │  ← Business Logic, Services
├─────────────────────────────────────┤
│       Infrastructure Layer          │  ← Data Access, Repositories
└─────────────────────────────────────┘
```

- **表示层**：负责 UI 渲染和用户交互
- **核心层**：包含核心业务逻辑和服务接口
- **基础设施层**：处理数据持久化和外部服务集成

---

## 从源码构建

### 前置条件

1. **安装 .NET 10 SDK**
   - 下载地址：https://dotnet.microsoft.com/download/dotnet/10.0
   - 验证安装：
     ```powershell
     dotnet --version
     # 应输出 10.0.300 或更高
     ```

2. **安装 Visual Studio 2022** (可选，推荐)
   - 工作负载：".NET 桌面开发"
   - 单个组件：".NET 10 SDK"

### 构建步骤

#### 1. 克隆仓库
```powershell
git clone https://github.com/你的用户名/QianYueTang.CLI.git
cd QianYueTang.CLI
```

#### 2. 还原 NuGet 包
```powershell
dotnet restore QianYueTang.CLI.slnx
```

> **注意**：如果遇到 NuGet 还原问题（特别是在 .NET 10 预览版），请参考 [常见问题](#常见问题)。

#### 3. 编译项目
```powershell
dotnet build QianYueTang.CLI.slnx --configuration Release
```

#### 4. 运行应用程序
```powershell
dotnet run --project QianYueTang.CLI/QianYueTang.CLI.csproj
```

### 发布独立版本

#### 发布 Windows 版本（自包含）
```powershell
dotnet publish QianYueTang.CLI/QianYueTang.CLI.csproj `
  --configuration Release `
  --runtime win-x64 `
  --self-contained true `
  --output ./publish `
  /p:PublishSingleFile=true
```

#### 发布便携版本
```powershell
dotnet publish QianYueTang.CLI/QianYueTang.CLI.csproj `
  --configuration Release `
  --runtime win-x64 `
  --self-contained false `
  --output ./publish-portable
```

---

## 使用指南

### 功能模块

#### 1. 设备管理
1. 点击左侧导航栏的 "设备" 图标
2. 在设备列表上方点击 "扫描" 按钮
3. 等待扫描完成，设备将自动显示在列表中
4. 点击设备可查看详细信息

#### 2. SSH 终端
1. 在设备列表中双击某个设备
2. 在弹出的对话框中输入 SSH 凭据
3. 连接成功后，将打开终端窗口

#### 3. 数据包捕获
1. 点击顶部菜单的 "工具" → "数据包捕获"
2. 选择网络适配器
3. 点击 "开始捕获" 按钮
4. 捕获的数据包将实时显示在列表中

#### 4. 配置管理
1. 点击左侧导航栏的 "设置" 图标
2. 在设置页面中可以：
   - 修改应用程序主题
   - 配置 SSH 默认端口
   - 管理保存的连接配置

---

## 配置说明

### appsettings.json

应用程序配置文件位于：
- 开发环境：`QianYueTang.CLI/appsettings.json`
- 生产环境：`%APPDATA%\QianYueTang.CLI\appsettings.json`

#### 示例配置

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "Database": {
    "ConnectionString": "Data Source=qianyuetang-cli.db"
  },
  "Ssh": {
    "DefaultPort": 22,
    "ConnectionTimeout": 30
  },
  "PacketCapture": {
    "MaxPackets": 10000,
    "DefaultSnapshotLength": 65536
  }
}
```

### 自定义主题

应用程序使用 MaterialDesignInXAML，可以在 `App.xaml` 中修改主题：

```xml
<materialDesign:BundledTheme 
    BaseTheme="Light" 
    PrimaryColor="DeepPurple" 
    SecondaryColor="Lime" />
```

可选的主色调：
- `DeepPurple`（默认）
- `Blue`
- `Teal`
- `Green`
- `Orange`
- `Red`

---

## 常见问题

### 1. NuGet 还原失败（.NET 10）

**问题**：运行 `dotnet restore` 时出现 `Value cannot be null. (Parameter 'path1')` 错误。

**解决方案**：
- 这是 .NET 10 SDK 的已知 bug
- 临时解决方案：
  1. 从备份目录复制 `obj/project.assets.json`
  2. 或使用 Visual Studio 2022 的 NuGet 包管理器还原

### 2. 运行时出现 XamlParseException

**问题**：应用程序启动时崩溃，提示找不到资源。

**解决方案**：
- 确保 `App.xaml` 中正确引用了所有资源字典
- 检查 `Presentation/Styles/` 文件夹下的 XAML 文件是否存在
- 重新编译项目

### 3. 数据包捕获无法工作

**问题**：点击 "开始捕获" 按钮无反应。

**可能原因**：
- 没有管理员权限
- 网络适配器不支持混杂模式
- WinPcap/Npcap 未安装

**解决方案**：
1. 以管理员身份运行应用程序
2. 安装 [Npcap](https://npcap.com/)（推荐）或 WinPcap
3. 在设置中选择正确的网络适配器

### 4. SSH 连接失败

**问题**：无法连接到远程设备。

**排查步骤**：
1. 检查设备 IP 地址和端口是否正确
2. 确认网络连接正常（ping 测试）
3. 检查防火墙设置
4. 查看应用程序日志（`%APPDATA%\QianYueTang.CLI\logs\`）

---

## 贡献指南

我们欢迎任何形式的贡献！

### 报告 Bug

1. 前往 [Issues](https://github.com/Murasameprogram/QianYueTang.CLI/issues) 页面
2. 点击 "New Issue"
3. 选择 "Bug Report" 模板
4. 填写详细信息，包括：
   - 复现步骤
   - 期望行为
   - 实际行为
   - 截图（如果有）

### 提出新功能

1. 前往 [Issues](https://github.com/Murasameprogram/QianYueTang.CLI/issues) 页面
2. 点击 "New Issue"
3. 选择 "Feature Request" 模板
4. 描述新功能的用途和预期行为

### 提交代码

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

### 代码规范

- **C# 代码**：遵循 [Microsoft C# Coding Conventions](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-guidelines)
- **XAML 代码**：使用 4 空格缩进，属性按字母顺序排列
- **提交信息**：使用 [Conventional Commits](https://www.conventionalcommits.org/) 规范

---

## 开源协议

本项目采用 **MIT 协议** - 详见 [LICENSE](LICENSE) 文件。

---

## 致谢

### 开源项目

- [MaterialDesignInXAML](https://github.com/MaterialDesignInXAML/MaterialDesignInXamlToolkit) - Material Design 风格控件库
- [CommunityToolkit.Mvvm](https://github.com/CommunityToolkit/dotnet) - MVVM 框架
- [SSH.NET](https://github.com/sshnet/SSH.NET) - SSH 客户端库
- [SharpPcap](https://github.com/chmorgan/sharppcap) - 数据包捕获库
- [PacketDotNet](https://github.com/chmorgan/packetnet) - 数据包解析库

### 开发工具

- [Visual Studio 2022](https://visualstudio.microsoft.com/)
- [.NET 10 SDK](https://dotnet.microsoft.com/)
- [SQLite](https://www.sqlite.org/)

---

## 联系方式

- **项目主页**：[https://github.com/Murasameprogram/QianYueTang.CLI](https://github.com/Murasameprogram/QianYueTang.CLI)
- **问题反馈**：[Issues](https://github.com/Murasameprogram/QianYueTang.CLI/issues)
- **电子邮件**：b051813@163.com

---

## 更新日志

### v1.0.0 (2026-05-18)

#### 新增功能
- ✨ 初始版本发布
- ✨ 网络设备发现和管理
- ✨ LLDP 协议分析
- ✨ SSH 终端仿真
- ✨ 数据包捕获和分析
- ✨ SQLite 数据库集成
- ✨ Material Design 风格界面

#### 修复问题
- 🐛 修复资源字典引用错误
- 🐛 修复 XAML 编译错误
- 🐛 修复转换器资源引用问题

---

**巴斯塔胡空间站** 
**千月堂项目组** <br>
**2026/5/18**
