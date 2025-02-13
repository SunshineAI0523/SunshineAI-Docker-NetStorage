# SunshineAI-Docker-NetStorage

一个基于Docker容器技术的智能网络存储解决方案,集成了多种常用网盘、下载工具和智能家居服务。

## 技术栈

- **容器化技术**
  - Docker
  - DevContainer
  - GitHub Actions自动构建

- **存储服务**
  - Cloudreve (文件管理与分享)
  - AList (多存储引擎聚合)
  - MinIO (对象存储服务)

- **智能家居**
  - Home Assistant (智能家居控制中心)

- **下载工具**
  - Aria2 (多协议下载器)
  - qBittorrent (BT下载工具)
  - Transmission (轻量级BT客户端)

## 功能特点

### 1. 统一存储管理
- 多种存储服务集成(Cloudreve/AList/MinIO)
- 统一的文件管理界面
- 支持多种存储协议
- 灵活的权限控制

### 2. 智能下载中心
- 支持多种下载协议(HTTP/FTP/BT/磁力链接等)
- 多任务并行下载
- 自动分类存储
- 远程控制管理

### 3. 智能家居集成
- Home Assistant智能家居控制
- 设备自动发现
- 场景自动化
- 远程监控管理

### 4. 系统特性
- 基于DevContainer的开发环境
- 多架构支持(AMD64/ARM64)
- 自动化构建与部署
- 容器化隔离运行
- 简单的配置管理

## 目录结构

```
.
├── .devcontainer/          # 开发容器配置
├── .github/workflows/      # GitHub Actions工作流
├── scripts/               # 辅助脚本
└── README.md              # 项目说明文档
```

## 快速开始

1. 克隆仓库
```bash
git clone https://github.com/yourusername/SunshineAI-Docker-NetStorage.git
```

2. 使用VSCode打开项目,并重新打开至容器中

3. 等待容器构建完成后即可使用

## 服务访问

- Home Assistant: `http://localhost:8123`
- Cloudreve: `http://localhost:5212`
- AList: `http://localhost:5244`
- MinIO: `http://localhost:9000`
- MinIO Console: `http://localhost:9001`

## 环境要求

- Docker 20.10+
- VSCode + Remote Container插件
- 8GB+ RAM建议
- 20GB+ 可用磁盘空间

## 开发相关

- 支持VSCode DevContainer开发环境
- 集成代码规范检查
- 自动化测试与构建
- 容器镜像自动发布

## 贡献指南

欢迎提交Issue和Pull Request来帮助改进项目。

## 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

## 相关项目

- [Home Assistant](https://www.home-assistant.io/)
- [Cloudreve](https://github.com/cloudreve/Cloudreve)
- [AList](https://github.com/alist-org/alist)
- [MinIO](https://min.io/)
```