# cs-ipv6-nat-toolkit
专为C-SERVERS服务器设计的IPv6 NAT工具 - 自动计算端口范围，生成socat转发命令，支持Delta1 Frankfurt等服务器一键配置

# C-SERVERS IPv6 NAT 工具包

[![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![最后提交时间](https://img.shields.io/github/last-commit/k08255-lxm/cs-ipv6-nat-toolkit)

[English Version](README_en.md) | 中文版

## 🚀 在线访问
👉 **[点击这里立即使用](http://cs-ipv6-nat-toolkit.github.pcbbs.net/)** 👈

## 🚀 功能特性
- **智能端口计算引擎**  
  基于IPv6地址末段十六进制值自动计算TCP/UDP端口范围
- **双栈转发命令生成**  
  一键生成即用型socat转发命令，支持：
  - IPv4→IPv6 TCP/UDP转发
  - IPv6→IPv4 TCP/UDP转发
- **服务器预设配置**  
  内置Delta1 Frankfurt服务器配置（NAT IP: 62.113.198.26）
- **企业级网络支持**  
  自动生成systemd服务配置，支持开机自启
- **多语言界面**  
  中英文双语自由切换

## 🖥️ 快速开始
### 1. 安装必要依赖
#### 安装 socat
根据操作系统选择以下命令：

```bash
# CentOS/RHEL
sudo yum install -y socat

# Ubuntu/Debian
sudo apt-get update && sudo apt-get install -y socat

# Alpine Linux
sudo apk add socat
```

#### 验证安装
```bash
socat -V
# 应显示类似 socat version 1.7.4.0 的信息
```

### 2. 使用工具
#### 在线使用
直接访问 [在线工具页面](http://cs-ipv6-nat-toolkit.github.pcbbs.net/)

#### 本地使用
```bash
git clone https://github.com/k08255-lxm/cs-ipv6-nat-toolkit.git
cd cs-ipv6-nat-toolkit
# 用浏览器打开 index.html
```

### 3. 运行转发命令
示例命令（替换为工具生成的端口）：
```bash
# TCP转发示例
socat TCP4-LISTEN:10000,reuseaddr,fork TCP6:[2a00:f48:1000:416::11]:10000

# UDP转发示例
socat UDP4-LISTEN:13000,reuseaddr,fork UDP6:[2a00:f48:1000:416::11]:13000
```

### 4. 持久化配置（推荐）
```bash
# 创建systemd服务文件
sudo tee /etc/systemd/system/socat-10000.service <<EOF
[Unit]
Description=Socat Port Forwarding (TCP 10000)
After=network.target

[Service]
ExecStart=/usr/bin/socat TCP4-LISTEN:10000,reuseaddr,fork TCP6:[2a00:f48:1000:416::11]:10000
Restart=always

[Install]
WantedBy=multi-user.target
EOF

# 启用服务
sudo systemctl enable socat-10000
sudo systemctl start socat-10000
```

### 5. 防火墙配置
```bash
# 开放TCP端口
sudo ufw allow 10000/tcp

# 开放UDP端口
sudo ufw allow 13000/udp

# 查看规则
sudo ufw status
```

## 📖 详细使用指南
### 步骤1：输入IPv6地址
支持格式：
- 完整格式：`2a00:f48:1000:416:0000:0000:0000:5401`
- 简写格式：`2a00:f48:1000:416::5401`

### 步骤2：选择服务器
| 选项 | 说明 |
|------|------|
| Delta1 Frankfurt | 自动填充预设NAT IP (62.113.198.26) |
| 自定义服务器 | 手动输入其他NAT IP |

### 步骤3：获取配置
生成结果包含：
```bash
# 端口范围
TCP: 225040-225049
UDP: 121800-121804

# 示例命令（自动填充）
socat TCP4-LISTEN:225040,reuseaddr,fork TCP6:[2a00:f48:1000:416::5401]:225040

# 持久化配置命令
sudo systemctl enable socat-225040
```

## 🛠️ 故障排查
### 常见问题
#### "socat: command not found"
- 确认已正确安装socat
- 重新运行安装命令

#### "Address already in use"
```bash
# 查找占用进程
sudo lsof -i :10000

# 终止进程
sudo kill -9 <PID>
```

#### "Permission denied"
- 使用root权限运行命令
```bash
sudo socat ...
```

## 🛠️ 开发者指南
### 项目结构
```
cs-ipv6-nat-toolkit/
├── index.html          # 核心逻辑
├── LICENSE             # 许可证文件
├── README.md           # 中文文档
├── README_en.md        # 英文文档
└── docs/               # 文档资源
    └── preview.png     # 界面预览
```

### 扩展开发
欢迎通过以下方式贡献代码：
1. 提交Issue报告问题
2. Fork仓库进行功能开发
3. 发起Pull Request

## 🙏 鸣谢
本工具由 [DeepSeek](https://www.deepseek.com) 智能引擎辅助开发

## 🔌 该项目所支持的服务商
[![C-SERVERS](https://img.shields.io/badge/Deepseek制作-C--SERVERS-blue)](https://c-servers.co.uk)

## 📜 许可证
MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

## 🖼️ 界面预览
![工具界面](docs/preview.png)
