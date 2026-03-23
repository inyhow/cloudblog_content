---
title: "Windows 11 环境下 OpenClaw 源码安装指南 (D 盘版)"
description: ""
category: ""
tags:
  - openclaw
status: published
reviewNote: ""
pinned: false
coverImage: ""
pubDate: 2026-03-23T05:07:37.679Z
updatedDate: 2026-03-23T05:07:37.679Z
affiliate: false
template: 
customData: {}
editorMode: wysiwyg
---

对于希望在 Win11 下进行深度定制或保持系统盘（C 盘）整洁的用户，将 [OpenClaw](https://github.com/openclaw/openclaw.git) 安装在 D 盘是一个非常明智的选择。

## 一、 前置环境准备

在开始之前，请确保你的系统已安装以下工具：

* **Node.js**: 推荐 **v24** 或更高版本（最低支持 v22.16+）。
* **pnpm**: 现代化的包管理工具（通过 `npm install -g pnpm` 安装）。
* **Git for Windows**: 用于克隆代码及提供 Bash 环境。

---

## 二、 源码克隆与依赖安装

打开 **PowerShell**，进入你的 D 盘根目录：

1. **克隆仓库**：
   **PowerShell**

   ```
   cd D:\
   git clone https://github.com/openclaw/openclaw.git
   cd openclaw
   ```
2. **配置 pnpm 全局目录 (可选)**： 为了避免全局命令报错，建议将 pnpm 的工具链也设在 D 盘：
   **PowerShell**

   ```
   pnpm config set global-bin-dir "D:\Program Files\nodejs\pnpm_global"
   ```
3. **安装项目依赖**：
   **PowerShell**

   ```
   pnpm install
   ```

   > **注意**：如果在安装 `node-llama-cpp` 等原生模块时报错，请确保已安装 [Visual Studio Build Tools](https://www.google.com/search?q=https://visualstudio.microsoft.com/visual-cpp-build-tools/)，或使用 `pnpm install --ignore-scripts` 跳过原生编译。
   >

---

## 三、 编译构建

OpenClaw 是一个多模块项目，需要先构建前端 UI，再构建核心服务。在 Windows 下建议**分步执行**：

1. **构建 UI 界面**：
   **PowerShell**

   ```
   pnpm ui:build
   ```
2. **构建核心程序**：
   **PowerShell**

   ```
   pnpm build
   ```

   当看到 `[copy-hook-metadata] Copied...` 字样时，说明构建已成功。

---

## 四、 初始化与运行

构建完成后，你需要通过“登机检查（Onboard）”来配置你的管理员账号和数据库：

1. **启动引导程序**：
   **PowerShell**

   ```
   node bin/openclaw.mjs onboard
   ```
2. **按照提示操作**：

   * **设置邮箱/密码**：用于登录本地 Web 后台。
   * **数据库**：初次使用建议选择 **SQLite**，它会直接保存在 D 盘的项目文件夹内。
   * **安装守护进程**：选择 `Yes` 可以让 OpenClaw 随系统自启动。
3. **验证状态**： 运行以下命令检查一切是否正常：
   **PowerShell**

   ```
   node bin/openclaw.mjs doctor
   ```

---

## 五、 进阶：如何访问后台

一旦引导完成，OpenClaw 的 **Gateway** 服务会自动启动。

* **Web 面板地址**：通常为 `http://localhost:3000`（或你在 onboard 过程中定义的端口）。
* **管理工具**：你可以通过该界面接入各类 AI 模型（如 DeepSeek, GPT-4）或配置电商自动化插件。

---

## 💡 维护小贴士

* **如何更新**：由于是源码安装，更新时只需在 `D:\openclaw` 执行 `git pull`，然后重新运行 `pnpm install && pnpm build`。
* **环境变量问题**：如果提示“找不到 openclaw 命令”，请将 `D:\Program Files\nodejs\pnpm_global` 手动添加到 Win11 的**系统环境变量 Path** 中。
