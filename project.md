# Terminal Reader

## 项目概述

跨平台局域网文件传输应用，支持同一局域网内设备之间通过 mDNS 自动发现并进行高速文件传输。

## 目标平台

- Android
- iOS
- Windows
- macOS
- Linux

## 核心功能

### 设备发现
- **mDNS 自动发现**: 同一局域网内的设备自动互相发现（基于 `_terminal-reader._tcp.local` 服务类型）
- **手动连接**: 支持手动输入 IP 地址和端口连接设备

### 文件传输
- **传输方式**: 局域网内通过原始 TCP Socket 直连传输
- **协议**: 自定义二进制协议（Header: 文件名长度 + 文件名 + 文件大小 → Body: 文件数据）
- **默认端口**: 9876

### 后续扩展
- 架构预留云端中转能力，后续可支持跨网络传输

## 技术方案

| 层级 | 方案 |
|------|------|
| 框架 | Flutter |
| mDNS 发现 | multicast_dns (纯 Dart) |
| TCP 传输 | dart:io (ServerSocket/Socket) |
| 文件选择 | file_picker |
| 本地 IP | network_info_plus |
| 存储路径 | path_provider |
| 权限管理 | permission_handler |
| 状态管理 | provider |

## 项目结构

```
lib/
  main.dart
  models/
    device_info.dart
    file_info.dart
    transfer_task.dart
  services/
    mdns_discovery_service.dart
    tcp_server_service.dart
    tcp_client_service.dart
    file_transfer_coordinator.dart
  providers/
    app_state.dart
  screens/
    home_screen.dart
    devices_tab.dart
    transfers_tab.dart
    settings_screen.dart
    manual_add_dialog.dart
    file_picker_sheet.dart
  widgets/
    device_card.dart
    transfer_progress_card.dart
    status_indicator.dart
    empty_state.dart
  utils/
    constants.dart
    ip_utils.dart
    file_utils.dart

apps/                  # 应用入口目录
modules/               # 业务模块目录
packages/              # 基础功能目录（公共组件、工具库、基础设施等）
```

## Android 配置

- 已添加阿里云 Maven 仓库镜像（`maven.aliyun.com/repository/google` 和 `maven.aliyun.com/repository/public`）
