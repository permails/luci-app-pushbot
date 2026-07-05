# luci-app-pushbot (English)

[中文文档](README.md)

"PushBot" is a router status push notification plugin designed specifically for OpenWrt. It can push real-time information such as router IP changes, device online/offline status, CPU load, and device temperature directly to your various terminal devices.

## Acknowledgments & Declaration
The birth and continuous improvement of this plugin are inseparable from the contributions of the following open-source community authors. We extend our most sincere gratitude to:
- **[tty228](https://github.com/tty228/luci-app-serverchan)**: This plugin was originally developed based on `luci-app-serverchan`.
- **[zzsj0928](https://github.com/zzsj0928/luci-app-pushbot)**: When the limitations of the original WeChat push became apparent, it was refactored into `luci-app-pushbot`, expanding to include DingTalk, WeCom, and many other push channels.
- In this latest refactoring, built upon previous work, a **comprehensive Internationalization (i18n) standardization** has been implemented. All hardcoded Chinese characters have been completely removed, allowing the plugin to perfectly adapt to the language preferences of users across different countries and regions.

## 🌟 Latest Feature: Comprehensive i18n Support
Following the latest underlying refactoring, PushBot now fully adheres to OpenWrt's standard multi-language development specifications:
- **Web UI Localization**: All page text has been extracted into standard `.po` translation files, which automatically switch based on the current LuCI system language setting (e.g., if the system is in English, the plugin interface is fully English).
- **Backend Push Message Localization**: The script layer also implements dynamic language adaptation. When the router's backend detects a device dropping offline or an IP change, it reads the `luci.main.lang` setting to push message content that matches your interface language (say goodbye to receiving Chinese alerts on an English system).

## Supported Push Platforms
This plugin supports the vast majority of mainstream notification platforms:
- **DingTalk Bot** (钉钉机器人)
- **WeCom Bot / WeCom App** (企业微信)
- **Feishu Bot** (飞书机器人)
- **PushPlus** (Supports pushing to WeChat Official Accounts and group pushes)
- **Bark** (A custom notification service designed for iOS users, supporting custom icons/sounds)
- **PushDeer** (An app-less push service based on Apple App Clips)
- **Custom Webhook** (DIY interface, easily compatible with platforms like Telegram Bot, ServerChan, etc.)

## Core Features
- **Device Online/Offline Notifications**: Accurately pushes device alias, MAC address, and online time.
- **Traffic Abnormalities & Statistics**: Keep track of the traffic consumption of individual devices at any time.
- **Router Status Monitoring**: Alerts for IP/IPv6 address changes, high CPU temperature, and high system load.
- **Security Alerts**: Warnings for frequent SSH/Web login failures to prevent brute-force attacks.
- **Highly Customizable Do-Not-Disturb (DND) & Scheduled Tasks**.

## Installation & Dependencies
Because this plugin uses active probing to detect device connections, it must rely on the following components. Please ensure you have updated your router's software sources before installing:
- Core dependencies: `iputils-arping`, `curl`, `jq`
- Traffic statistics feature dependency: `wrtbwmon` (may conflict with some Flow Offloading configurations; install according to your situation).

### How to Compile:
```bash
git clone https://github.com/permails/luci-app-pushbot package/luci-app-pushbot
```
And ensure this is enabled in your `.config` configuration file:
```
CONFIG_PACKAGE_luci-app-pushbot=y
```

## Notes
- Using active probing avoids frequent false online/offline reports caused by device WiFi sleep. If your device experiences instability due to frequent sleeping, please adjust the timeout parameters in "Advanced Settings".
- When retrieving device names, the script reads `/var/dhcp.leases`. Devices with static IPs or behind a secondary router may not be able to obtain a hostname automatically. It is recommended to manually configure the "Device Alias (MAC Whitelist/Blacklist)" feature in the plugin.

---
*Issues and Pull Requests (PRs) are always welcome!*
