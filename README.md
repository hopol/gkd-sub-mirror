# GKD 订阅镜像仓库

[![同步状态](https://github.com/hopol/gkd-sub-mirror/actions/workflows/sync.yml/badge.svg)](https://github.com/hopol/gkd-sub-mirror/actions/workflows/sync.yml)
[![镜像发布](https://github.com/hopol/gkd-sub-mirror/actions/workflows/release.yml/badge.svg)](https://github.com/hopol/gkd-sub-mirror/actions/workflows/release.yml)
[![许可证](https://img.shields.io/badge/license-GPL--3.0-blue.svg)](LICENSE)

## 简介

这是 [Lin-arm/GKD_subscription](https://github.com/Lin-arm/GKD_subscription) 的自动镜像仓库。

**GKD 订阅** 是 [GKD](https://github.com/gkd-kit/gkd) 客户端的自动跳过广告订阅规则，覆盖 963 个应用、2381 个规则组。

**本项目不做任何修改**，仅提供：
- 📦 **源码同步**：每5天自动备份上游源代码
- 🚀 **发布镜像**：自动镜像上游的离线订阅文件
- 📝 **中文日志**：每个版本附带中文更新说明

## 为什么需要镜像？

GitHub 上的开源项目可能因为维护调整、作者归档等原因变得不可访问。本镜像仓库确保即使上游项目出现问题，源码和订阅文件仍然可用。

## 下载

前往 [Releases](https://github.com/hopol/gkd-sub-mirror/releases) 页面下载最新版本。

| 文件 | 说明 |
|------|------|
| `gkd-subscription-offline-id667-v{版本}.json5` | 离线订阅文件（导入 GKD 即可使用） |

## 订阅源地址

| 源 | 地址 | 国内可用 |
|---|---|---|
| CF 源 | `https://gkd667.vv.ax/gkd.json5` | ✅ |
| CloudFlare Pages | `https://gkd-subscription-667.pages.dev/gkd.json5` | ✅ |
| GitHub | `https://raw.githubusercontent.com/Lin-arm/GKD_subscription/main/dist/gkd.json5` | ❌ 需翻墙 |

## 工作原理

### 源码同步（每5天）

```
上游仓库 (Lin-arm/GKD_subscription)
    ↓ git fetch
对比提交哈希
    ↓ 有变化
git archive 导出 → upstream/
    ↓
提交 & 推送 & 创建标签
```

### 发布镜像（每5天检查）

```
检查上游最新 Release
    ↓
是否已镜像？
    ├─ 是 → 跳过
    └─ 否 ↓
下载离线订阅文件
    ↓
生成中文 Changelog + 原始日志
    ↓
创建镜像 Release（mirror-v{版本号}）
```

## 标签说明

| 标签格式 | 说明 | 示例 |
|----------|------|------|
| `mirror-v{版本}-{哈希}` | 源码同步标签 | `mirror-v556-abc1234` |
| `mirror-{版本}` | 发布镜像标签 | `mirror-556` |

## 项目结构

```
gkd-sub-mirror/
├── .github/
│   └── workflows/
│       ├── sync.yml           # 源码同步工作流（每5天）
│       └── release.yml        # 发布镜像工作流（每5天检查）
├── upstream/                  # 上游源码（运行时生成）
├── sync.sh                    # 本地同步脚本
├── README.md                  # 本文档
├── .gitignore
└── LICENSE
```

## 本地同步

```bash
git clone https://github.com/hopol/gkd-sub-mirror.git
cd gkd-sub-mirror
git remote add upstream https://github.com/Lin-arm/GKD_subscription.git
chmod +x sync.sh
./sync.sh
```

## 上游项目信息

- **项目名称**：GKD_subscription
- **上游仓库**：https://github.com/Lin-arm/GKD_subscription
- **订阅 ID**：667
- **覆盖应用**：963 个
- **规则组数**：2381 个应用规则组 + 3 个全局规则组
- **上游许可证**：GPL-3.0
- **GKD 客户端**：https://github.com/gkd-kit/gkd

## 许可证

本镜像仓库采用 [GPL-3.0 许可证](LICENSE)，与上游项目一致。

## 致谢

感谢 [Lin-arm](https://github.com/Lin-arm) 维护的 GKD 订阅规则项目，以及 [gkd-kit](https://github.com/gkd-kit) 创建的 GKD 客户端。
