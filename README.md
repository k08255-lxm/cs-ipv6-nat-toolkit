# cs-ipv6-nat-toolkit
专为C-SERVERS服务器设计的IPv6 NAT工具 - 自动计算端口范围，生成socat转发命令，支持Delta1 Frankfurt等服务器一键配置

# C-SERVERS IPv6 NAT 工具包

[![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![最后提交时间](https://img.shields.io/github/last-commit/k08255-lxm/cs-ipv6-nat-toolkit)

[English Version](README_en.md) | 中文版

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
```bash
git clone https://github.com/k08255-lxm/cs-ipv6-nat-toolkit.git
cd cs-ipv6-nat-toolkit
# 使用浏览器打开 index.html
```

## 📖 详细使用指南
### 步骤1：输入IPv6地址
支持完整格式或简写格式：
- 完整格式：`2a00:f48:1000:416:0000:0000:0000:5401`
- 简写格式：`2a00:f48:1000:416::5401`

### 步骤2：选择服务器
| 选项 | 说明 |
|------|------|
| Delta1 Frankfurt | 自动填充预设NAT IP |
| 自定义服务器 | 手动输入其他NAT IP |

### 步骤3：获取配置
生成结果包含：
```bash
# 端口范围
TCP: 225040-225049
UDP: 121800-121804

# 示例命令（自动填充实际端口）
socat TCP4-LISTEN:225040,reuseaddr,fork TCP6:[2a00:f48:1000:416::5401]:225040

# 持久化服务配置
sudo systemctl enable socat-225040
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

