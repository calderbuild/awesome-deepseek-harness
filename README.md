# Awesome DeepSeek Harness

A curated list of DeepSeek Harness (`dsh`) resources: official documentation, core concepts, npm packages, community plugins, and third-party write-ups.

Unofficial community list, not affiliated with DeepSeek. DeepSeek Harness is in developer preview and ships compatibility-breaking changes; the links below point at the `master` branch unless noted.

## Quick start

```sh
npx @deepseek-ai/dsh web
```

Requires Node.js. Starts the Web UI at `http://127.0.0.1:3080`.

## Official resources

- [Repository](https://github.com/deepseek-ai/deepseek-harness)
- [README.zh](https://github.com/deepseek-ai/deepseek-harness/blob/master/README.zh.md)
- [Discord community](https://discord.gg/Ycq5dCaS4)
- [GitHub Discussions](https://github.com/deepseek-ai/deepseek-harness/discussions)
- [WeCom group survey (Chinese)](https://trtgsjkv6r.feishu.cn/share/base/form/shrcnIt5twSVdLGD52KJBckGCgg)
- [`dsh-plugin` topic](https://github.com/topics/dsh-plugin)
- [AGENTS.md](https://github.com/deepseek-ai/deepseek-harness/blob/master/AGENTS.md)
- [CONTRIBUTING.md](https://github.com/deepseek-ai/deepseek-harness/blob/master/CONTRIBUTING.md)
- [THIRD_PARTY_NOTICES.md](https://github.com/deepseek-ai/deepseek-harness/blob/master/THIRD_PARTY_NOTICES.md)

## Official documentation

Paths are relative to `docs/` in the main repository. Most files have a `.zh.md` counterpart.

- [Architecture](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md): plugin tree, profiles and bundles, turn flow, session log, capability seams
- [Cordis primer](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cordis-primer.md): the underlying plugin framework
- [Cordis tutorial](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cordis-tutorial/index.md)
- [Development guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/development.md)
- [Web UI guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.md)
- [Python SDK guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/python-sdk.md)
- [Agent lifecycle](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/agent-lifecycle.md)
- [Tool execution pipeline](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/tool-execution-pipeline.md)
- [Capability seams](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/capability-seams.md)
- [Event producer/consumer map](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/event-producer-consumer.md)
- [Config catalog](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/config-catalog.md)
- [Tool catalog](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/tool-catalog.md)
- [Persistence catalog](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/persistence-catalog.md)
- [Extension cookbook](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cookbook/extension-cookbook.md)
- [Testing](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/testing.md)
- [Glossary](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/glossary.md)

## Core concepts

- Everything is a plugin: the model adapter, tool registry, session log, sandbox and approval policy, agent loop, and Web UI are all plugins on [Cordis](https://github.com/cordiverse/cordis).
- Profiles, bundles, and patch layers compose the boot tree; `dsh --profile web --dump-config` prints the tree a machine actually boots.
- Event-sourced session log: append-only `SessionEvent` stream, with a runtime invariant that anything model-visible is reconstructable from the log. Replay, fork, resume, transcripts, and telemetry derive from it.
- Capability seams have three roles: service definition, provider, consumer. Swapping a provider moves a whole capability, for example Bash, PTY, and LSP to a remote sandbox together.
- Agent presets are per-session compositions. Built-in presets shipped in the repo: `minimal`, `standard`, `code`, `cordis`.

## Official npm packages

- [@deepseek-ai/dsh](https://www.npmjs.com/package/@deepseek-ai/dsh): CLI, profile boot, plugin management, browser UI alias
- [@deepseek-ai/dsh-web-app](https://www.npmjs.com/package/@deepseek-ai/dsh-web-app): browser surface bundle
- [@deepseek-ai/dsh-headless](https://www.npmjs.com/package/@deepseek-ai/dsh-headless): one-shot runner with no HTTP layer
- [@deepseek-ai/dsh-frontend](https://www.npmjs.com/package/@deepseek-ai/dsh-frontend): built frontend distribution

## Run from source

```sh
git clone https://github.com/deepseek-ai/deepseek-harness.git
cd deepseek-harness
pnpm install
pnpm run build
pnpm dsh web
```

## Community plugins

Collected from the `dsh-plugin` topic on 2026-08-13. Inclusion here does not imply endorsement.

| Repository | What it does |
|---|---|
| [zhu1090093659/dsh-web-ui](https://github.com/zhu1090093659/dsh-web-ui) | Web UI skins and panels: task board, git graph, side panels, mobile UI, token stats |
| [AdamPlatin123/awesome-dsh-plugins](https://github.com/AdamPlatin123/awesome-dsh-plugins) | Plugin directory with daily compatibility tracking |
| [Anionex/dsh-vision-toolkit](https://github.com/Anionex/dsh-vision-toolkit) | Vision features for text-only models: image Q&A, long-screenshot OCR, UI grounding |
| [0xsline/awesome-deepseek-harness](https://github.com/0xsline/awesome-deepseek-harness) | Sibling curated list of plugins, tools, and infrastructure |
| [ccch1mneyyy/dsh-cc-tui](https://github.com/ccch1mneyyy/dsh-cc-tui) | Fullscreen terminal UI in Claude Code style |
| [huiliyi37/dsh-tianshu-tui](https://github.com/huiliyi37/dsh-tianshu-tui) | Terminal UI for DeepSeek Harness |

## Third-party write-ups

- [首发体验 | DeepSeek Harness 来了，它不想做下一个 Codex](https://www.ifanr.com/1675083), iFanr hands-on review (Chinese)
- [对标 Claude Code：DeepSeek Harness 公测，同步开放 npm 插件生态](https://m.ithome.com/html/989446.htm), ITHome news (Chinese)
- [DeepSeek Harness 即将公测，模型厂商的 Agent 框架是怎么造的](https://segmentfault.com/a/1190000048154707), SegmentFault architecture explainer (Chinese)
- [DeepSeek 为什么必须做 Harness](https://m.163.com/news/article/L4727P0I00097U7T.html), 163 analysis (Chinese)

## Related

- [cordiverse/cordis](https://github.com/cordiverse/cordis): the meta-framework powering dsh
- [cordiverse/paper](https://github.com/cordiverse/paper): A Programming Paradigm for Spatiotemporal Composability
- [DeepSeek API docs](https://api-docs.deepseek.com/)

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). One addition per pull request, with a working link and a one-line description. Keep it factual and on topic.

## License

This list is [MIT](LICENSE). Every listed project keeps its own license.
