# OpenList 一键安装管理脚本

一个功能完整的 OpenList 安装和管理脚本，支持一键安装、自动更新、版本管理等功能。

[![GitHub release](https://img.shields.io/github/release/OpenListTeam/OpenList.svg)](https://github.com/OpenListTeam/OpenList/releases)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Linux-green.svg)](https://github.com/ypq123456789/openlist)

## 🚀 快速开始

### 下载并安装
#### 一键下载命令
```curl -fsSL "https://raw.githubusercontent.com/ypq123456789/openlist/refs/heads/main/openlist.sh" -o openlist.sh && chmod +x openlist.sh```

#### 下载脚本
```curl -fsSL "https://raw.githubusercontent.com/ypq123456789/openlist/refs/heads/main/openlist.sh" -o openlist.sh```

#### 设置执行权限
```chmod +x openlist.sh```

#### 运行脚本（交互式）
```sudo ./openlist.sh```

## 📋 系统要求

- **操作系统**: Linux (支持 systemd)
- **架构**: x86_64 (amd64) 或 arm64
- **权限**: Root 权限 (安装时需要)
- **依赖**: curl, tar
- **可选**: jq (用于更好的 JSON 解析)

### 支持的 Linux 发行版

- Ubuntu 16.04+
- Debian 9+  
- CentOS 7+
- RHEL 7+
- Fedora 30+
- 其他支持 systemd 的 Linux 发行版

## ✨ 功能特性

### 🔧 核心功能
- **一键安装**: 支持快速安装 OpenList
- **版本选择**: 支持 beta 版本和自定义版本
- **自动更新**: 智能检查并更新到最新版本
- **服务管理**: 完整的 systemd 服务管理
- **配置管理**: 自动化配置文件和数据目录管理

### 🛠️ 管理功能
- **交互式菜单**: 用户友好的命令行界面
- **日志查看**: 实时查看服务日志
- **状态监控**: 检查服务运行状态
- **版本信息**: 显示当前安装版本和更新历史
- **完整卸载**: 彻底清理所有文件和配置

### 🌐 网络功能
- **代理支持**: 支持 GitHub 代理加速下载
- **重试机制**: 网络故障自动重试
- **多源下载**: 支持多个下载源

## 📖 使用说明

### 命令行使用

```bash
# 显示交互式菜单
sudo ./openlist.sh

# 安装到默认目录 (/opt/openlist)
sudo ./openlist.sh install

# 安装到自定义目录
sudo ./openlist.sh install /path/to/custom/directory

# 更新 OpenList
sudo ./openlist.sh update

# 检查更新
sudo ./openlist.sh check-update

# 卸载 OpenList
sudo ./openlist.sh uninstall
```

### 交互式菜单

脚本提供了友好的交互式菜单界面：

```
欢迎使用 OpenList 管理脚本 (Beta版本支持)

1、安装 OpenList
2、更新 OpenList  
3、卸载 OpenList
-------------------
4、查看状态
5、查看版本
6、检查更新
-------------------
7、启动 OpenList
8、停止 OpenList
9、重启 OpenList
-------------------
10、查看日志
-------------------
0、退出脚本
```

## 🎯 版本管理

### 支持的版本类型

1. **Beta 版本** (推荐)
   - 最新功能和改进
   - 定期更新
   - 相对稳定

2. **自定义版本**
   - 指定特定的版本标签
   - 适合生产环境

### 版本选择示例

```bash
# 安装时会提示选择版本
请选择要安装的版本：
1、beta (推荐 - 最新功能)
2、查看所有可用版本
3、手动输入版本标签
```

## 🔄 自动更新

### 设置自动更新

```bash
# 创建定时任务
sudo crontab -e

# 添加每日凌晨2点检查更新 (推荐)
0 2 * * * /path/to/openlist.sh check-update >/dev/null 2>&1

# 或者每周检查更新
0 2 * * 0 /path/to/openlist.sh check-update >/dev/null 2>&1
```

### 手动检查更新

```bash
# 检查是否有新版本
sudo ./openlist.sh check-update

# 如果有更新，脚本会提示是否立即更新
发现新的beta版本更新！
是否立即更新？[Y/n]:
```

## 📁 安装目录结构

```
/opt/openlist/                 # 默认安装目录
├── openlist                   # 主程序二进制文件
├── data/                      # 数据目录
│   ├── config.json           # 配置文件
│   ├── data.db               # 数据库文件
│   └── log/                  # 日志目录
└── .version                  # 版本信息文件
```

## 🌐 网络配置

### 使用代理

如果您的网络环境需要代理访问 GitHub：

```bash
# 安装时会提示
是否使用 GitHub 代理？（默认无代理）
代理地址必须为 https 开头，斜杠 / 结尾
例如：https://ghproxy.com/
请输入代理地址或直接按回车继续:
```

### 常用代理地址

- `https://ghproxy.com/`
- `https://mirror.ghproxy.com/` 
- `https://gh.api.99988866.xyz/`

## 🔍 故障排除

### 常见问题

**1. 下载失败**
```bash
# 检查网络连接
curl -I https://github.com

# 尝试使用代理
curl -fsSL "https://ghproxy.com/https://raw.githubusercontent.com/ypq123456789/openlist/refs/heads/main/openlist.sh" | bash -s install
```

**2. 权限错误**
```bash
# 确保使用 root 权限
sudo ./openlist.sh install
```

**3. 服务启动失败**
```bash
# 查看服务状态
sudo systemctl status openlist

# 查看详细日志
sudo journalctl -u openlist -f
```

**4. 端口占用**
```bash
# 检查端口占用
sudo netstat -tlnp | grep 5244

# 或使用 ss
sudo ss -tlnp | grep 5244
```

### 日志位置

- **服务日志**: `sudo journalctl -u openlist`
- **应用日志**: `/opt/openlist/data/log/`
- **安装日志**: 脚本运行时的标准输出

## 🔐 安全说明

### 默认配置

- **默认端口**: 5244
- **默认用户**: admin
- **初始密码**: 安装时自动生成并显示

### 安全建议

1. **修改默认密码**: 首次登录后立即修改密码
2. **防火墙配置**: 适当配置防火墙规则
3. **定期更新**: 保持软件版本最新
4. **备份数据**: 定期备份配置和数据

## 📞 技术支持

### 获取帮助

- **GitHub Issues**: [提交问题](https://github.com/ypq123456789/openlist/issues)
- **官方文档**: [OpenList 文档](https://github.com/OpenListTeam/OpenList)

### 日志收集

在提交问题时，请提供以下信息：

```bash
# 系统信息
uname -a
cat /etc/os-release

# 服务状态
sudo systemctl status openlist

# 服务日志
sudo journalctl -u openlist --no-pager -l

# 版本信息
cat /opt/openlist/.version
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

### 开发

```bash
# 克隆仓库
git clone https://github.com/ypq123456789/openlist.git
cd openlist

# 编辑脚本
vim openlist.sh

# 测试
sudo ./openlist.sh install
```

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## 🙏 致谢

- [OpenList Team](https://github.com/OpenListTeam/OpenList) - 提供优秀的 OpenList 项目
- 所有贡献者和用户的反馈和建议

---

**⭐ 如果这个脚本对您有帮助，请给个 Star！**
