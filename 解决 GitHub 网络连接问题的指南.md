# README: 解决 GitHub 网络连接问题的指南

## 概述
本指南提供了在使用 Git 操作时，与 GitHub 网络连接出现问题时的排查和解决方案。按照以下步骤可以诊断并修复潜在问题。

---

## 第一步：验证网络连接

1. **安装 `ping` 工具**  
   确保系统中已安装 `ping` 工具，运行以下命令：
   ```bash
   apt-get update
   apt-get install -y iputils-ping
   ```

2. **测试网络连接**  
   使用以下命令检查是否可以正常连接到 GitHub：
   ```bash
   ping github.com
   ```
   - 如果能收到响应，说明基础网络连接正常。
   - 如果没有响应，请检查网络设置或防火墙配置。

---

## 第二步：增加 Git 操作的超时时间

有时由于 Git 操作的超时时间过短，会导致操作失败。通过以下步骤增加超时时间：

1. **增加 HTTP 缓冲区大小**
   ```bash
   git config --global http.postBuffer 524288000
   ```

2. **取消低速连接的限制**
   ```bash
   git config --global http.lowSpeedLimit 0
   ```

3. **增加低速超时时间**
   ```bash
   git config --global http.lowSpeedTime 999
   ```

通过这些设置，可以减少因网络缓慢或不稳定导致的中断问题。

---

## 使用说明

完成上述步骤后，重新尝试执行 Git 操作。如果问题仍未解决，请检查其他网络配置或 Git 设置是否正确。  
此文档可以分享给其他遇到类似问题的人。
