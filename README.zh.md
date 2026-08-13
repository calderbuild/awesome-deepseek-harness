# Awesome DeepSeek Harness [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

DeepSeek Harness（`dsh`）是 DeepSeek AI 开源的 agent harness，一切皆插件，底层是 Cordis。

## 目录

- [快速开始](#快速开始)
- [官方资源](#官方资源)
- [文档](#文档)
- [核心概念](#核心概念)
- [包](#包)
- [社区插件](#社区插件)
- [解读](#解读)
- [相关列表](#相关列表)

## 快速开始

```sh
npx @deepseek-ai/dsh web
```

需要 Node.js。启动后的 Web UI 在 `http://127.0.0.1:3080`。

从源码运行：

```sh
git clone https://github.com/deepseek-ai/deepseek-harness.git
cd deepseek-harness
pnpm install
pnpm run build
pnpm dsh web
```

## 官方资源

- [仓库](https://github.com/deepseek-ai/deepseek-harness) - 源码、issue 和 release。
- [中文 README](https://github.com/deepseek-ai/deepseek-harness/blob/master/README.zh.md) - 官方中文说明。
- [Discord 社区](https://discord.gg/Ycq5dCaS4) - 官方 Discord。
- [GitHub Discussions](https://github.com/deepseek-ai/deepseek-harness/discussions) - 反馈和 bug 报告。
- [企微入群问卷](https://trtgsjkv6r.feishu.cn/share/base/form/shrcnIt5twSVdLGD52KJBckGCgg) - 官方企微群入群表单。
- [`dsh-plugin` 话题](https://github.com/topics/dsh-plugin) - 插件仓库的发现入口。
- [AGENTS.md](https://github.com/deepseek-ai/deepseek-harness/blob/master/AGENTS.md) - 面向 agent 的仓库规则。
- [CONTRIBUTING.md](https://github.com/deepseek-ai/deepseek-harness/blob/master/CONTRIBUTING.md) - 向上游贡献的方式。
- [第三方依赖声明](https://github.com/deepseek-ai/deepseek-harness/blob/master/THIRD_PARTY_NOTICES.md) - 第三方依赖许可证。

## 文档

路径相对主仓库的 `docs/`，多数文件有 `.zh.md` 中文版。

- [架构](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.zh.md) - 插件树、profile 与 bundle、turn 流程、会话日志、能力 seam。
- [Cordis 入门](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cordis-primer.zh.md) - 底层插件框架介绍。
- [Cordis 教程](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cordis-tutorial/index.md) - 分步教程。
- [开发指南](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/development.zh.md) - 如何在仓库上开发。
- [Web UI 指南](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.md) - Web UI 用法。
- [Python SDK 指南](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/python-sdk.md) - 内置 Python SDK。
- [Agent 生命周期](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/agent-lifecycle.zh.md) - turn 与 step 的执行序列。
- [工具执行管线](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/tool-execution-pipeline.zh.md) - 工具调用的执行方式。
- [能力 seam](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/capability-seams.zh.md) - 可替换能力模型。
- [事件生产消费图](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/event-producer-consumer.zh.md) - 每个事件的生产者和消费者。
- [配置目录](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/config-catalog.zh.md) - 配置字段。
- [工具目录](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/tool-catalog.zh.md) - 内置工具。
- [持久化目录](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/persistence-catalog.zh.md) - 存储布局。
- [扩展 cookbook](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cookbook/extension-cookbook.md) - 扩展 dsh 的配方。
- [测试](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/testing.zh.md) - 测试实践。
- [术语表](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/glossary.zh.md) - 术语定义。

## 核心概念

- 一切皆插件：模型适配器、工具注册表、会话日志、沙箱与审批策略、agent loop、Web UI 都是跑在 [Cordis](https://github.com/cordiverse/cordis) 上的插件。
- Profile、Bundle 与 patch 层组合出启动时的插件树；`dsh --profile web --dump-config` 能打印一台机器实际启动的完整配置。
- 事件溯源会话日志：append-only 的 `SessionEvent` 流，运行时强制"模型可见即可从日志重建"，回放、fork、resume、转录、遥测都从这条流推导。
- 能力 seam 由三角色组成：service definition、provider、consumer，换一个 provider 可以整体切换一种能力，比如把 Bash、PTY、LSP 一起指向远程沙箱。
- Agent 预设是每个会话独立的组合，内置四个：`minimal`、`standard`、`code`、`cordis`。

## 包

- [@deepseek-ai/dsh](https://www.npmjs.com/package/@deepseek-ai/dsh) - CLI，负责 profile 启动、插件管理和浏览器 UI 入口。
- [@deepseek-ai/dsh-web-app](https://www.npmjs.com/package/@deepseek-ai/dsh-web-app) - 浏览器端 bundle。
- [@deepseek-ai/dsh-headless](https://www.npmjs.com/package/@deepseek-ai/dsh-headless) - 无 HTTP 层的单次执行 runner。
- [@deepseek-ai/dsh-frontend](https://www.npmjs.com/package/@deepseek-ai/dsh-frontend) - 编译后的前端产物。

## 社区插件

- [zhu1090093659/dsh-web-ui](https://github.com/zhu1090093659/dsh-web-ui) - Web UI 皮肤和面板：任务板、Git graph、侧边面板、移动端界面、token 统计。
- [Anionex/dsh-vision-toolkit](https://github.com/Anionex/dsh-vision-toolkit) - 给纯文本模型加视觉能力：图片问答、长截图 OCR、UI 定位。
- [ccch1mneyyy/dsh-cc-tui](https://github.com/ccch1mneyyy/dsh-cc-tui) - Claude Code 风格的全屏终端界面。
- [huiliyi37/dsh-tianshu-tui](https://github.com/huiliyi37/dsh-tianshu-tui) - DeepSeek Harness 终端界面。

## 解读

- [首发体验 | DeepSeek Harness 来了，它不想做下一个 Codex](https://www.ifanr.com/1675083) - 爱范儿上手评测。
- [对标 Claude Code：DeepSeek Harness 公测，同步开放 npm 插件生态](https://m.ithome.com/html/989446.htm) - IT之家报道。
- [DeepSeek Harness 即将公测，模型厂商的 Agent 框架是怎么造的](https://segmentfault.com/a/1190000048154707) - SegmentFault 架构解读。
- [DeepSeek 为什么必须做 Harness](https://m.163.com/news/article/L4727P0I00097U7T.html) - 网易科技分析。

## 相关列表

- [Awesome DSH Plugins](https://github.com/AdamPlatin123/awesome-dsh-plugins) - 插件目录，带每日兼容性追踪。
- [Awesome DeepSeek Harness](https://github.com/0xsline/awesome-deepseek-harness) - 插件、工具和基础设施精选。
- [Awesome](https://github.com/sindresorhus/awesome) - awesome 列表总目录。

## 参与贡献

见 [contributing.md](contributing.md)。

## 脚注

- 非官方社区清单，与 DeepSeek 无关。
- DeepSeek Harness 处于开发者预览阶段，会有破坏性兼容变更，链接指向 `master` 分支。
- 社区插件快照收集于 2026-08-13。
