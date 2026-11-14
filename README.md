<div align="center">

# Video Prompts Skills

**从一个创意或一段文字，写出完整的中文视频生成提示词。**

先想清楚整片怎么表达，再设计每个片段的镜头、表演与声音。

[技能入口](./SKILL.md) · [完整案例](./examples/classroom-drawing.md) · [拍法对照](./examples/rehearsal-key.md) · [镜头语言](./references/camera-language.md)

[![Agent Skill](https://img.shields.io/badge/Agent%20Skill-video--prompts--skills-4F46E5)](./SKILL.md)
[![Prompt Types](https://img.shields.io/badge/Prompts-MiniMax%20H3%20%7C%20Seedance%20%7C%20General-111827)](#支持的提示词类型)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-10B981)](./LICENSE)

</div>

---

## 这是什么？

Video Prompts Skills 是一套面向 AI 助手的视频提示词创作技能。给它一个视频想法、一段小说或散文，它会梳理人物、事件与表达意图，完成分段、分镜、动作、表演和声音设计，输出可以逐段复制使用的中文提示词。

支持 **MiniMax H3、Seedance 2.5 和通用视频提示词**，也可以用来优化已有提示词、转换模型写法、分析优秀案例，或根据实际成片修正偏差。

长内容会先规划整片，再按动作、对白和反应所需时间拆分，默认每段不超过 **15 秒**。每个生成片段可以包含多个镜头，前后保持人物、道具、空间与声音的衔接；短内容按需要结束，不必填满15秒。

技能包含导演表达、经典运镜、人物调度、剪辑、声画关系和动作连续性等参考方法。AI 按任务需要读取资料，将方法用于具体内容，最终交付完整提示词。

## 安装

使用 [Skills CLI](https://github.com/vercel-labs/skills) 安装，需要 Node.js 与 npx。以下命令为全局安装；移除 `-g` 可安装到当前项目。

### Codex

```bash
npx skills add https://github.com/kuschzzp/video-prompts-skills -g --skill video-prompts-skills -a codex
```

### Claude Code

```bash
npx skills add https://github.com/kuschzzp/video-prompts-skills -g --skill video-prompts-skills -a claude-code
```

### OpenCode

```bash
npx skills add https://github.com/kuschzzp/video-prompts-skills -g --skill video-prompts-skills -a opencode
```

### 安装到多个客户端

```bash
npx skills add https://github.com/kuschzzp/video-prompts-skills -g --skill video-prompts-skills -a codex -a claude-code -a opencode
```

### 从本地仓库安装

在仓库根目录执行：

```bash
npx skills add ./ -g --skill video-prompts-skills -a codex
```

### 更新与卸载

更新全局安装的技能：

```bash
npx skills update video-prompts-skills -g -y
```

卸载全局安装的技能：

```bash
npx skills remove video-prompts-skills -g -y
```

项目级安装的更新使用 `-p` 替代 `-g`；卸载时移除 `-g`。更多选项见 [Skills CLI 命令说明](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)。

## 快速开始

安装后，直接告诉 AI 你想做什么。在支持 `$技能名` 调用的客户端中，可以这样使用：

```text
使用 $video-prompts-skills，把下面的创意写成 Seedance 2.5 中文视频提示词。
画幅16:9，单段不超过15秒，输出所有片段的完整提示词。

【粘贴你的视频创意】
```

也可以处理文学改编、已有提示词或成片问题：

```text
使用 video-prompts-skills，把下面的小说片段改编为 MiniMax H3 中文视频提示词。
保留原始对白，先说明可以拆成多少段、各段预计多长，再输出每段完整提示词。

使用 video-prompts-skills，优化下面的提示词。
保留剧情和对白，重点检查镜头衔接、动作是否成立，以及15秒内能否完成。

使用 video-prompts-skills，把下面的 H3 提示词转换为 Seedance 2.5 写法。
保留人物、事件和素材用途，按目标类型重新组织。

使用 video-prompts-skills，分析这段视频与提示词的偏差。
人物接过物品时出现了重复动作，请定位问题并修改对应片段。
```

没有安装时，也可以让能读取本地文件的 AI 助手直接读取本仓库的 `SKILL.md`，并按需读取引用资料。请保留完整目录结构。

调用后，技能按以下顺序工作：

1. **确认类型**：选择 MiniMax H3、Seedance 或通用版。没有指定时先询问；当前对话已有选择时沿用。
2. **理解与构思**：提取原文约束，确定整片视角、信息揭示、情绪推进和声画基调。
3. **估时与分段**：按内容容量安排生成片段，说明段数、内容和预计时长。
4. **设计与交付**：完成镜头、调度、表演与声音设计，检查连续性，逐段输出完整正文。

详细流程见 [SKILL.md](./SKILL.md)。普通创作只需给出想法和已有要求，无需填写制作表或通读所有参考文件。

## 支持的提示词类型

| 类型 | 输出方式 | 适合的需求 |
| --- | --- | --- |
| MiniMax H3 | 中文镜头正文，保留 `[Shot N]`、说话人及对白等必要标签，按需提供声音字段 | 需要分镜、对白与声画协同设计的 H3 创作 |
| Seedance 2.5 | 中文画面与时间段描述，交代动作、表演、声音及实际素材用途 | Seedance 创作、多镜头组织和参考素材使用 |
| 通用版 | 中文自然语言描述，不加入模型专用标签 | 尚未选定模型，或需要进一步适配其他入口 |

H3 默认交付中文创作稿；官方完整重写格式或 API 请求体需要按具体入口另行适配。15秒是默认分段预算，用户指定时长或平台另有限制时据此调整。

每段提示词独立成块，保留必要的人物、场景和起始状态，时间从0开始。对白默认保留原文，无内容的字段直接省略；多段交付不使用“同上”或大纲替代后续正文。

## 查看示例

| 示例 | 可以看到什么 |
| --- | --- |
| [美术教室里的儿童画](./examples/classroom-drawing.md) | 从原始创意到两个14秒片段，展示完整的 H3 与 Seedance 提示词 |
| [排练室交钥匙的三种拍法](./examples/rehearsal-key.md) | 同一人物关系、事件与对白，分别用固定观察、贴近反应和拉开空间组织镜头 |

两个案例均为原创教学示范。可以用它们了解完整交付的样子，以及同一事件为什么会选择不同的拍法。

## 项目结构

```text
video-prompts-skills/
├── SKILL.md                           # 技能入口与工作流程
├── agents/
│   └── openai.yaml                    # 技能展示信息
├── references/
│   ├── directing-and-performance.md   # 导演表达与表演设计
│   ├── camera-language.md             # 景别、构图与经典运镜
│   ├── editing-and-staging.md         # 视点、人物调度与剪辑
│   ├── visual-continuity.md           # 可读性、空间与连续性
│   ├── action-and-assets.md           # 动作逻辑与参考素材
│   ├── shot-and-sound-design.md       # 时间预算、分段与声音
│   ├── lighting-and-color.md          # 光影、色温与调色板
│   ├── object-and-reversal.md         # 以物件为先、意义翻转
│   ├── movement-and-checklist.md      # 运镜决策与交稿前自查
│   ├── segment-checks.md              # 多段数数自查：自包含、节拍预算、运镜计数、歌词对位、因果、状态一致、入口上限
│   ├── minimax-h3.md                  # MiniMax H3 适配
│   ├── seedance-2.5.md                # Seedance 2.5 适配
│   └── result-diagnosis.md            # 成片诊断与修订
├── examples/
│   ├── classroom-drawing.md           # 完整分段与双模型示例
│   └── rehearsal-key.md               # 同场戏的三种拍法
├── assets/
│   ├── shot-card.md                   # 可选镜头卡
│   └── iteration-record.md            # 可选迭代记录
├── README.md
└── LICENSE
```

## 新增参考

- [光影与色彩](./references/lighting-and-color.md)：光源、方向、软硬、色温对照、时段与调色板，以及光如何承载意义。
- [以物件为先](./references/object-and-reversal.md)：一个日常物件先行、问句开场、三拍、两种对立解读、一句金句、留白结尾；含原创练习《7:42》填表示范。
- [运镜决策与自查](./references/movement-and-checklist.md)：每镜只一个运镜的决策表，及交稿前自查清单。
- [多段数数自查](./references/segment-checks.md)：分段生成没有段间记忆，自包含禁跨段指代、节拍预算、运镜计数、歌词对位、因果、状态一致、入口上限，七条逐项数数；来自《收到收到》MV 第 1、2 段的真实失败。
- Seedance 2.5 适配已修订：15 秒交付预算与单次生成上限的区别、16:9 与 9:16 的选择、负向写法；新增能力数字于 2026-11-14 对官方模型页与 ModelArk 教程复核（单次 4–30 秒、480p / 720p / 1080p、24fps、可延长两次），消费端入口档位仍以实际入口为准。

## 手动验证与反馈

用实际创作任务验证输出，再结合所用平台的成片检查效果。重点看原文信息是否保留、片段时长是否合理、关键动作是否清楚，以及镜头与声音能否共同完成表达。

反馈时请附上原始需求、提示词类型、模型或平台版本、完整提示词，以及具体偏差。涉及成片时，提供对应片段与时间点，方便定位需要修改的描述。[迭代记录](./assets/iteration-record.md) 可用于保存对比结果。

本仓库目前以手动测试和成片反馈迭代，暂未提供自动化评测套件或量化基准。实际视频生成由所用平台完成。

## 开发与维护

修改技能时，在 [SKILL.md](./SKILL.md) 维护任务识别、读取路径与交付流程；具体方法放在 `references/`，完整教学案例放在 `examples/`，可选制作模板放在 `assets/`。

新增或调整规则后，用实际输入检查完整流程：能否选对类型、读到所需资料、合理分段，并输出每段可独立使用的提示词。修改模型适配时，同时核对中文正文、必要标签、声音字段与素材引用。

本地 `temp/` 用于开发参考，已加入忽略规则，技能运行不依赖该目录。

## 许可证

本项目采用 [Apache License 2.0](./LICENSE)。
