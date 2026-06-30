# iOS Location Spoofer

用代理软件的 HTTPS 解密功能，把 Apple 地图定位骗到世界任何角落。

## 怎么回事

iPhone 看 Wi-Fi 信号和基站信号，拿着 BSSID 列表去问 Apple 这些设备在什么位置。Apple 回一份坐标清单，iOS 根据这些坐标算出自己在哪里。

这套配置做的事情很简单：**在 Apple 发回坐标的路上拦截下来，全部改成你想要的数字**。iPhone 拿到改造过的坐标，算出来就是你指定的地方。

## 支持哪些软件

| 软件 | 文件 | 导入方法 |
|------|------|---------|
| Shadowrocket（小火箭） | `ios-location-spoofer.sgmodule` | 配置 → 模块 → 右上角 + |
| Surge | `ios-location-spoofer.sgmodule` | 首页 → 模块 → 安装新模块 |
| Loon | `ios-location-spoofer.lnplugin` | 设置 → 插件 → 添加插件 |
| Quantumult X | `ios-location-spoofer.snippet` | 设置 → 重写 → 添加 |
| Stash | `ios-location-spoofer.stoverride` | 覆写 → 安装覆写 |

## 怎么用

1. 软件里打开 HTTPS 解密 / MITM 开关
2. 安装并信任 CA 证书（设置 → 通用 → VPN 与设备管理 → 安装 → 证书信任设置 → 启用）
3. 导入模块文件，勾上启用
4. 断开重连 VPN，开关定位服务
5. 打开地图 App 验证

## 改坐标

默认 Apple Park（37.3349, -122.00902）。在模块参数里改：

```
latitude=39.9042&longitude=116.4074
```

参数：

| 名字 | 默认值 | 说明 |
|------|--------|------|
| `latitude` | 37.3349 | 目标纬度 |
| `longitude` | -122.00902 | 目标经度 |
| `horizontalAccuracy` | 39 | 水平精度 |
| `verticalAccuracy` | 1000 | 垂直精度 |
| `altitude` | 530 | 海拔 |
| `failOpen` | true | 出错放行原数据 |
| `debug` | false | 调试日志 |

## 文件清单

```
ios-location-spoofer.sgmodule    # Shadowrocket / Surge
ios-location-spoofer.lnplugin    # Loon
ios-location-spoofer.snippet     # Quantumult X
ios-location-spoofer.stoverride  # Stash
location-spoofer.js              # 核心脚本（四平台共用）
location-spoofer-qx.js           # QX 专用
location-spoofer-config.json     # 配置样板
```
