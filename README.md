# content-publish-ops — 内容发布运营团 Swarm Skill

把"对外发布"这件容易翻车的事，变成一条**可追踪、可审计、带硬门禁**的流水线。

> 适用框架：WorkSwarm / JiuwenSwarm（Swarm Skills Hub），并兼容 Agent Skills 开放标准（Claude Code / Cursor 零适配可跑）。

## 它解决什么

对外发内容最怕三件事：
1. **漏敏感 / 泄密钥**
2. **质检没过就发出去**
3. **发错渠道 / 发错版本还没记录**

本 Swarm 用 **5 个专职角色 + 1 个主理人**，把「素材汇总 → 内容整理 → 内容生成 → 加严质检 → 多渠道发布」跑成严格串行的流水线，每条发布都留痕。

## 角色一览

| 角色 | 代号 | Phase | 职责 |
|------|------|-------|------|
| 主理人 | team-lead（潘布达） | 编排 | 建队 / 消息中转 / 最终签发，角色间不得直连 |
| 素材汇总员 | content-collector（全汇齐） | 1 | 素材汇总 |
| 内容整理员 | content-organizer（理得顺） | 2 | 去敏 / 整理 / 版本化 |
| 内容生成员 | content-creator（章既成） | 3 | 按渠道生成发布稿 |
| 加严质检官 | content-qa-officer（甄无瑕） | 4 | 加严质检，唯一放行闸门 |
| 发布管理员 | publish-manager（布全道） | 5 | 多渠道发布 + 发布台账 |

## 两条铁门禁（不可绕过）

- **① 质检门禁（G1）**：Phase 4 结论非「通过」不得进入 Phase 5。
- **② 确认门禁（G2）**：Phase 5 发布前，必须逐条向用户确认「发什么 / 发到哪 / 版本号」，获明确同意才发。

另有内部**链路纪律（G3）**：每阶段完整原文转交下一阶段，角色不互连、不跳级。

## 预设工作流

- **W1 全流程发布**：Phase 1 → 2 → 3 → 4 → 5（严格串行，给素材要发对外）
- **W2 发布前加严检查**：仅 Phase 4（已有成稿只查错）
- **W3 快速发布**：仅 Phase 5（已审核只发）
- **W4 发布台账管理**：查《发布记录》（问发过什么）

## 包结构（Swarm Skill 5 文件 + 角色）

```
content-publish-ops-swarm-skill/
├── SKILL.md            # 入口：元数据 + 概述 + 路由(W1-W4) + 两条铁门禁
├── workflow.md         # Mermaid 编排图 + Phase1→5 + 质检/确认/链路三道闸
├── bind.md             # 行为铁律(消息中转/不代写/不跳级/密钥不进对话) + 失败处理
├── dependencies.yaml   # 依赖工具与 6 角色声明
└── roles/
    ├── team-lead.md
    ├── content-collector.md
    ├── content-organizer.md
    ├── content-creator.md
    ├── content-qa-officer.md   # 含 7 大类检查项定义（含版权三件套）
    └── publish-manager.md
```

## 本地使用

将本目录作为 Swarm Skill 加载到 WorkSwarm 运行时即可；角色与门禁由 `bind.md` / `workflow.md` 在运行时强制。

## 提交到 Swarm Skills Hub

1. 在 GitHub 建公开仓并推送本目录（见仓库提交说明）。
2. 到 [Swarm Skills Hub](https://swarmskills.openjiuwen.com) 提交，归类「内容创作」。
3. Hub 描述中链接本 GitHub 仓库以便社区共建与溯源。

## License

MIT
