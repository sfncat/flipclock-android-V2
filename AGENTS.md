# AGENTS.md — flipclock-android-V2

## 项目是什么

Android 翻页时钟应用，基于开源 flipclock-android 的增强版（V2，当前 2.0.9）；在原版基础上增加自启动、防烧屏、天气、节气/三伏九九、竖排信息栏与自定义字体。

## 构建与入口

- 环境：JDK 21、Gradle 8.5（Wrapper 自带）、AGP 8.3.0、NDK r28（`28.2.13676358`）。
- 构建：`./gradlew assembleDebug`，产物 `app/build/outputs/apk/debug/app-debug.apk`；签名发布用 `scripts/build-release.ps1`（Windows）/ `scripts/build-release.sh`。
- 代码入口：主界面在 `app/src/main/java/com/stackof/flipclockv2`，SDL 胶水层在 `app/src/main/java/org/libsdl/app`；SDL2/SDL2_ttf 与原生代码已内嵌在 `app/jni/`，无需初始化子模块。

## 目录结构要点

- `app/`：Android 主模块（`src/main` 含 Java/res/assets/Manifest，`jni/` 为原生与 SDL）。
- `weather/`：天气功能 Gradle 模块，由根 `settings.gradle`（`include ':app', ':weather'`）引入。
- `docs/`：功能设计文档（自启动、冷启动空白卡片、防烧屏、日期/节气、竖排、天气）。
- `scripts/`：构建与开机链路脚本；`fonts/`、`keystore/`、`releases/` 分别存字体、签名配置与发布产物。

## 项目进度上报

- 本项目根目录的 `PROJECT_STATUS.md` 是进度上报文件，由本项目自己维护，供上层汇总只读取用。
- **每次改动收尾时更新**，不要等想起来再补。
- 结构：front matter（`project` / `path` / `status`(active|paused|done) / `owner_ai` / `updated`）+ 四段正文：`## 当前进展` / `## 等你决策` / `## TOP 待办` / `## 最近完成`。
- `## 当前进展` 一两句说清做到哪、卡在哪；`## 等你决策` 只放需要用户拍板的事，没有就写「暂无」，**这一段不许省略**；`## TOP 待办` 只放不依赖用户、AI 自己能推进的事，最多 5 条，行顺序即优先级；`## 最近完成` 倒序。
- 只写能确认的事实，未知写「待补充」，不编造。
- 动笔前先读规范：技能 `agents-md-authoring` 的 `references/project-status.md`。
