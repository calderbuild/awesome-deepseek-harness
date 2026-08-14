# Awesome DeepSeek Harness [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

DeepSeek Harness (`dsh`) is an open-source agent harness by DeepSeek AI where every part is a plugin, built on the Cordis meta-framework.

## Contents

- [Quick start](#quick-start)
- [Official resources](#official-resources)
- [Documentation](#documentation)
- [Core concepts](#core-concepts)
- [Packages](#packages)
- [Community plugins](#community-plugins)
- [Write-ups](#write-ups)
- [Related lists](#related-lists)

## Quick start

```sh
npx @deepseek-ai/dsh web
```

Requires Node.js. Starts the Web UI at `http://127.0.0.1:3080`.

To run from source:

```sh
git clone https://github.com/deepseek-ai/deepseek-harness.git
cd deepseek-harness
pnpm install
pnpm run build
pnpm dsh web
```

## Official resources

- [Repository](https://github.com/deepseek-ai/deepseek-harness) - Source code, issues, and releases.
- [README.zh](https://github.com/deepseek-ai/deepseek-harness/blob/master/README.zh.md) - Chinese README.
- [Discord community](https://discord.gg/Ycq5dCaS4) - Official Discord server.
- [GitHub Discussions](https://github.com/deepseek-ai/deepseek-harness/discussions) - Feedback and bug reports.
- [WeCom group survey (Chinese)](https://trtgsjkv6r.feishu.cn/share/base/form/shrcnIt5twSVdLGD52KJBckGCgg) - Entry form for the official WeCom group.
- [`dsh-plugin` topic](https://github.com/topics/dsh-plugin) - Plugin repositories tagged for discovery.
- [AGENTS.md](https://github.com/deepseek-ai/deepseek-harness/blob/master/AGENTS.md) - Rules for agents working on the repository.
- [CONTRIBUTING.md](https://github.com/deepseek-ai/deepseek-harness/blob/master/CONTRIBUTING.md) - How to contribute upstream.
- [THIRD_PARTY_NOTICES.md](https://github.com/deepseek-ai/deepseek-harness/blob/master/THIRD_PARTY_NOTICES.md) - Third-party dependency licenses.

## Documentation

Paths are relative to `docs/` in the main repository. Most files have a `.zh.md` counterpart.

- [Architecture](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md) - Plugin tree, profiles and bundles, turn flow, session log, and capability seams.
- [Cordis primer](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cordis-primer.md) - Introduction to the underlying plugin framework.
- [Cordis tutorial](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cordis-tutorial/index.md) - Step-by-step Cordis tutorial.
- [Development guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/development.md) - How to develop against the repository.
- [Web UI guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.md) - Using the Web UI.
- [Python SDK guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/python-sdk.md) - Bundled Python SDK.
- [Agent lifecycle](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/agent-lifecycle.md) - Turn and step sequence.
- [Tool execution pipeline](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/tool-execution-pipeline.md) - How tool calls run.
- [Capability seams](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/capability-seams.md) - Swappable capability model.
- [Event producer/consumer map](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/event-producer-consumer.md) - Every event and its producers and consumers.
- [Config catalog](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/config-catalog.md) - Configuration fields.
- [Tool catalog](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/tool-catalog.md) - Built-in tools.
- [Persistence catalog](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/persistence-catalog.md) - Storage layout.
- [Extension cookbook](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cookbook/extension-cookbook.md) - Recipes for extending dsh.
- [Testing](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/testing.md) - Test practices.
- [Glossary](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/glossary.md) - Terminology.

## Core concepts

- Everything is a plugin: the model adapter, tool registry, session log, sandbox and approval policy, agent loop, and Web UI are all plugins on [Cordis](https://github.com/cordiverse/cordis).
- Profiles, bundles, and patch layers compose the boot tree; `dsh --profile web --dump-config` prints the tree a machine actually boots.
- Event-sourced session log: an append-only `SessionEvent` stream with a runtime invariant that anything model-visible is reconstructable from the log. Replay, fork, resume, transcripts, and telemetry derive from it.
- Capability seams have three roles: service definition, provider, and consumer. Swapping a provider moves a whole capability, for example Bash, PTY, and LSP to a remote sandbox together.
- Agent presets are per-session compositions. Built-in presets: `minimal`, `standard`, `code`, and `cordis`.

## Packages

- [@deepseek-ai/dsh](https://www.npmjs.com/package/@deepseek-ai/dsh) - CLI, profile boot, plugin management, and browser UI alias.
- [@deepseek-ai/dsh-web-app](https://www.npmjs.com/package/@deepseek-ai/dsh-web-app) - Browser surface bundle.
- [@deepseek-ai/dsh-headless](https://www.npmjs.com/package/@deepseek-ai/dsh-headless) - One-shot runner with no HTTP layer.
- [@deepseek-ai/dsh-frontend](https://www.npmjs.com/package/@deepseek-ai/dsh-frontend) - Built frontend distribution.

## Community plugins
- [dhicoc/dsh-reverse-skill](https://github.com/dhicoc/dsh-reverse-skill) - Complete reverse-skill pack (85 SKILL.md) as a DeepSeek Harness Cordis plugin: reverse engineering, authorized pentesting and security-research skill router.

- [zhu1090093659/dsh-web-ui](https://github.com/zhu1090093659/dsh-web-ui) - Web UI skins and panels: task board, Git graph, side panels, mobile UI, and token stats.
- [Anionex/dsh-vision-toolkit](https://github.com/Anionex/dsh-vision-toolkit) - Vision features for text-only models: image Q&A, long-screenshot OCR, and UI grounding.
- [ccch1mneyyy/dsh-cc-tui](https://github.com/ccch1mneyyy/dsh-cc-tui) - Fullscreen terminal UI in Claude Code style.
- [huiliyi37/dsh-tianshu-tui](https://github.com/huiliyi37/dsh-tianshu-tui) - Terminal UI for DeepSeek Harness.
- [Nwflower/dsh-chat-import](https://github.com/Nwflower/dsh-chat-import) - Import Claude Code / Codex / ChatGPT / Cursor chat histories as resumable DeepSeek Harness sessions.

## Write-ups

- [首发体验 | DeepSeek Harness 来了，它不想做下一个 Codex](https://www.ifanr.com/1675083) - iFanr hands-on review (Chinese).
- [对标 Claude Code：DeepSeek Harness 公测，同步开放 npm 插件生态](https://m.ithome.com/html/989446.htm) - ITHome news (Chinese).
- [DeepSeek Harness 即将公测，模型厂商的 Agent 框架是怎么造的](https://segmentfault.com/a/1190000048154707) - SegmentFault architecture explainer (Chinese).
- [DeepSeek 为什么必须做 Harness](https://m.163.com/news/article/L4727P0I00097U7T.html) - 163 analysis (Chinese).

## Related lists

- [Awesome DSH Plugins](https://github.com/AdamPlatin123/awesome-dsh-plugins) - Plugin directory with daily compatibility tracking.
- [Awesome DeepSeek Harness](https://github.com/0xsline/awesome-deepseek-harness) - Curated plugins, tools, and infrastructure.
- [Awesome](https://github.com/sindresorhus/awesome) - The main list of awesome lists.

## Contributing

See [contributing.md](contributing.md).

## Footnotes

- Unofficial community list, not affiliated with DeepSeek.
- DeepSeek Harness is in developer preview with compatibility-breaking changes; links point at the `master` branch.
- Community plugin snapshot collected on 2026-08-13.