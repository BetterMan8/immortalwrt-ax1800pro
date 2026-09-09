# ImmortalWRT 京东云亚瑟 AX1800 Pro 自动编译固件

> 本项目基于 **ImmortalWRT 25.12** 稳定版，专为 **京东云亚瑟 AX1800 Pro（RE-SS-01）** 定制，通过 GitHub Actions 实现云端一键编译，无需本地搭建任何开发环境。

---

## 固件概览

| 项目 | 说明 |
|------|------|
| 系统版本 | ImmortalWRT 25.12（2026年7月发布的正式稳定版） |
| 目标设备 | 京东云亚瑟 AX1800 Pro（设备代号：RE-SS-01） |
| 主芯片平台 | 高通 IPQ60xx（四核 ARM Cortex-A53） |
| 包管理器 | **apk**（25.12 版本默认，替代了旧版的 opkg） |
| 固件格式 | SquashFS 只读文件系统（`.itb` 格式） |
| 管理界面 | LuCI Web 管理后台 + **Argon 暗色主题** |
| 科学代理 | **HomeProxy**（基于 sing-box 内核） |
| 硬件加速 | **高通 NSS 硬件加速**（完整驱动套件） |

---

## 预装软件包清单

### 主题与界面

- `luci-theme-argon`：Argon 暗色主题，界面美观现代
- `luci-app-argon-config`：Argon 主题个性化设置面板
- `luci-i18n-argon-config-zh-cn`：Argon 配置界面中文语言包
- `luci-i18n-base-zh-cn`：LuCI 基础界面中文语言包

### 科学代理（HomeProxy）

- `luci-app-homeproxy`：HomeProxy LuCI 管理界面
- `luci-i18n-homeproxy-zh-cn`：HomeProxy 中文语言包
- `sing-box`：高性能代理内核（支持多种协议）
- `kmod-tun`：TUN 虚拟网卡内核模块
- `kmod-inet-diag`：网络诊断内核模块
- `kmod-netlink-diag`：Netlink 诊断内核模块

### NSS 硬件加速驱动

- `kmod-qca-nss-drv`：NSS 核心驱动
- `kmod-qca-nss-dp`：NSS 数据面驱动
- `kmod-qca-nss-gmac`：NSS GMAC 驱动
- `kmod-qca-nss-drv-pppoe`：PPPoE 硬件加速
- `kmod-qca-nss-drv-l2tpv2`：L2TPv2 硬件加速
- `kmod-qca-nss-drv-pptp`：PPTP 硬件加速
- `kmod-qca-nss-drv-igs`：入站流量整形
- `kmod-qca-nss-drv-bridge-mgr`：桥接管理
- `kmod-qca-nss-drv-vlan-mgr`：VLAN 管理
- `kmod-qca-nss-macsec`：MACsec 加密支持
- `kmod-qca-nss-drv-netlink`：Netlink 接口

### 无线驱动

- `kmod-ath11k-ahb`：高通 ath11k AHB 总线无线驱动
- `kmod-ath11k-pci`：高通 ath11k PCI 总线无线驱动
- `ath11k-firmware-ipq6018`：IPQ6018 无线固件
- `ipq-wifi-jdcloud_re-ss-01`：京东云亚瑟专用 WiFi 校准数据

### 基础网络组件

- `firewall4`：第四代防火墙（基于 nftables）
- `nftables`：新一代包过滤框架
- `kmod-nft-offload`：nftables 硬件卸载支持
- `dnsmasq-full`：完整版 DNS/DHCP 服务器
- `ip-full`：完整 IP 路由工具集
- `ipv6helper`：IPv6 辅助配置工具
- `ppp`：点对点协议
- `ppp-mod-pppoe`：PPPoE 拨号模块
- `wpad-basic-mbedtls`：WPA/WPA2 认证守护进程
- `hostapd-common`：无线接入点守护进程

---

## 如何使用 GitHub Actions 编译固件

本仓库利用 GitHub 提供的免费云端服务器自动编译固件，整个过程无需在本地安装任何软件。

### 第一步：确认仓库文件

确保你的 GitHub 仓库中包含以下文件：

| 文件路径 | 说明 |
|----------|------|
| `.github/workflows/build.yml` | 编译工作流配置文件 |
| `.config` | AX1800 Pro 的编译配置文件 |
| `README.md` | 本说明文件 |

### 第二步：启动编译

1. 打开你的 GitHub 仓库页面。
2. 点击页面顶部的 **Actions**（行动）标签页。
3. 在左侧工作流列表中，点击 **Build ImmortalWRT for AX1800 Pro**。
4. 点击右侧绿色的 **Run workflow**（运行工作流）按钮。
5. 在弹出的下拉菜单中，确认分支为 `main`，然后点击绿色的 **Run workflow** 按钮。

### 第三步：等待编译完成

- 编译全程大约需要 **60 到 90 分钟**，具体取决于 GitHub 服务器的负载情况。
- 编译过程中，你可以随时在 Actions 页面点击运行记录，查看实时日志。
- 编译完成后，GitHub 会发送一封邮件通知你。
- 编译成功的标志是 Actions 页面显示绿色的勾 ✅。

---

## 如何下载编译好的固件

1. 在 Actions 页面，点击编译成功的那条运行记录（绿色勾 ✅）。
2. 页面滚动到最底部，找到 **Artifacts**（产物）区域。
3. 点击 **ImmortalWRT-AX1800-Pro-Firmware** 即可下载压缩包。
4. 解压后，你会看到以下两个核心文件：

| 文件名 | 用途说明 |
|--------|----------|
| `immortalwrt-25.12-...-squashfs-factory.itb` | **首次刷机**专用，从原厂固件刷入 ImmortalWRT 时使用 |
| `immortalwRT-25.12-...-squashfs-sysupgrade.itb` | **升级固件**专用，设备已运行 ImmortalWRT 时使用 |

> ⚠️ 注意：GitHub Actions 的 Artifacts 默认保留 **90 天**，过期后会自动删除，请及时下载。

---

## 刷机教程

### 首次刷机（从京东云原厂固件刷入 ImmortalWRT）

1. 用一根网线将电脑连接到路由器的 **LAN 口**（建议使用有线连接，避免无线中断导致刷机失败）。
2. 将电脑的 IP 地址手动设置为 `192.168.68.x` 网段（子网掩码 `255.255.255.0`，网关 `192.168.68.1`）。
3. 打开浏览器，访问 `192.168.68.1`，进入京东云原厂管理后台。
4. 找到 **系统设置 → 系统升级** 页面。
5. 点击"选择文件"，上传解压得到的 `*-factory.itb` 固件文件。
6. 点击"开始升级"，等待路由器自动重启。
7. 重启完成后，将电脑 IP 恢复为自动获取（DHCP）。
8. 访问 `192.168.1.1` 进入 ImmortalWRT 管理后台。

### 升级固件（从旧版 ImmortalWRT 升级到新版）

1. 登录 ImmortalWRT 管理后台（默认地址 `192.168.1.1`）。
2. 进入 **系统 → 备份/升级** 页面。
3. 在"刷写新的固件镜像"处，上传 `*-sysupgrade.itb` 文件。
4. 根据需要选择是否勾选 **保留配置**：
   - **勾选**：升级后保留当前的网络设置、密码等配置。
   - **不勾选**：恢复出厂设置，所有配置将被清除。
5. 点击"刷写"，等待路由器自动重启完成升级。

---

## 默认信息

| 项目 | 值 |
|------|-----|
| 默认管理地址 | `192.168.1.1` |
| 默认用户名 | `root` |
| 默认密码 | 首次登录时自行设置 |
| 默认无线名称（2.4G） | `ImmortalWRT` |
| 默认无线名称（5G） | `ImmortalWRT_5G` |

---

## 注意事项

- **刷机前务必备份**：刷机存在一定风险，建议提前备份原厂固件和重要配置。
- **使用有线连接**：首次刷机时务必使用网线连接，无线传输中断可能导致设备变砖。
- **不要中途断电**：刷机过程中切勿断电或关闭路由器，否则可能导致设备损坏。
- **NSS 加速说明**：NSS 硬件加速仅对桥接转发流量生效，经过 HomeProxy 代理的流量仍为软件转发，两者不冲突。
- **软件安装**：本固件为纯净版，仅预装了必要组件。如需额外软件，可在 LuCI 后台的"软件"页面使用 `apk install <包名>` 在线安装。
- **固件格式变更**：从 ImmortalWRT 24.10 版本开始，高通 IPQ60xx 平台的固件格式从传统的 `.bin` 变更为 `.itb`，这是正常现象。

---

## 常见问题

### 编译失败怎么办？

- 检查 `.config` 文件是否已正确上传到仓库根目录（文件名为 `.config`，前面有英文句号）。
- 检查 `build.yml` 中的分支名是否为 `openwrt-25.12`。
- 点击失败的 Actions 运行记录，查看日志中的红色报错信息。

### Artifacts 下载链接失效了？

- GitHub 免费账户的 Artifacts 默认保留 90 天，过期后需要重新编译。
- 你也可以在仓库的 Actions 页面重新触发一次编译。

### 刷机后无法访问后台？

- 确认电脑 IP 已恢复为自动获取（DHCP）。
- 尝试手动将电脑 IP 设为 `192.168.1.x` 网段。
- 按住路由器 Reset 按钮 10 秒恢复出厂设置后重试。

---

## 参考资料

- ImmortalWRT 官方仓库
- ImmortalWRT 官方文档
- HomeProxy 项目主页
- 京东云亚瑟 AX1800 Pro 设备信息

---

## 许可证

本仓库中的 `.config` 配置文件及 GitHub Actions 工作流脚本遵循 MIT 许可证。

固件源码遵循 ImmortalWRT / OpenWrt 项目各自的开源协议。
