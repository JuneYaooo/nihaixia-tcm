<div align="center">

# nihaixia

**把倪海厦中医课程整理成可检索、可追溯、有安全边界的 Agent Skill。**

Claude Code / Codex / OpenClaw Skill。装进 agent 后，可以用自然语言按症状、方剂、六经、课次或板书截图检索《伤寒论》课程资料，输出学习型辨证梳理、方证对比、逐课复习计划和截图证据索引。

[![GitHub stars](https://img.shields.io/github/stars/JuneYaooo/nihaixia?style=flat)](https://github.com/JuneYaooo/nihaixia/stargazers)
[![Skill](https://img.shields.io/badge/Agent-Skill-orange.svg)](./SKILL.md)
[![TCM](https://img.shields.io/badge/TCM-%E5%80%AA%E6%B5%B7%E5%8E%A6-green.svg)](./references/index.md)
[![Course](https://img.shields.io/badge/course-%E4%BC%A4%E5%AF%92%E8%AE%BA-blue.svg)](./references/lesson-map.md)

</div>

---

## 能做什么

- **白话问题入口**：把“感冒怕冷”“手脚冷”“拉肚子”“睡不着”等普通表达转成课程里的分水岭问题。
- **六经辨证导航**：按太阳、阳明、少阳、太阴、少阴、厥阴整理核心证候和传变逻辑。
- **方证对比**：围绕桂枝汤、麻黄汤、小柴胡汤、承气汤类、四逆汤辈等课程方证做鉴别。
- **症状索引**：从发热、便秘、下利、腹痛、失眠、手足冷等症状进入课程资料。
- **逐课复习**：15 讲《伤寒论》课程的主题地图、关键词和适合复习的问题。
- **截图证据**：649 张关键板书/PPT 截图索引，可按方名、课次、病机或时间点检索。
- **安全边界**：默认作为课程学习与中医理论整理，不做个人诊断、处方或剂量指导。

## 适合哪些场景

| 场景 | 适合程度 | 说明 |
| --- | --- | --- |
| 学习《伤寒论》课程 | 很适合 | 从课程地图、六经、方证、症状几个入口复习。 |
| 查某个方的课程方证 | 很适合 | 可返回症状群、病机层次、相关方和禁忌提醒。 |
| 用白话提问 | 很适合 | 先转成辨证分水岭，再进入课程术语。 |
| 找板书或 PPT 截图 | 适合 | 用 `scripts/search_screenshots.py` 检索截图索引。 |
| 整理学习笔记 | 适合 | 可生成可追加到 references 的 Markdown。 |
| 真实病情用药决策 | 不适合 | 本 skill 不提供个人诊断、处方、剂量或自我用药建议。 |

## 资料结构

| 文件 | 用途 |
| --- | --- |
| [`SKILL.md`](./SKILL.md) | Agent 触发描述、工作流和安全规则。 |
| [`references/index.md`](./references/index.md) | 总索引，告诉 agent 什么时候读取哪个模块。 |
| [`references/learning-entry.md`](./references/learning-entry.md) | 用户学习入口，按“学这个为了做什么”组织。 |
| [`references/beginner-questions.md`](./references/beginner-questions.md) | 白话问题入口，把普通表达转成辨证问题。 |
| [`references/six-channel.md`](./references/six-channel.md) | 六经辨证细模块。 |
| [`references/formula-patterns.md`](./references/formula-patterns.md) | 方剂方证与相关方对比。 |
| [`references/symptom-index.md`](./references/symptom-index.md) | 症状入口索引。 |
| [`references/lesson-map.md`](./references/lesson-map.md) | 15 讲逐课学习地图。 |
| [`references/screenshot-evidence.md`](./references/screenshot-evidence.md) | 649 张关键截图索引。 |
| [`scripts/search_screenshots.py`](./scripts/search_screenshots.py) | 截图证据排序检索脚本。 |

## 安装

### 方式一：让 AI 自己装

把下面这段 prompt 丢给你的 AI 助手：

```text
帮我安装 nihaixia skill：
https://github.com/JuneYaooo/nihaixia
```

agent 可以 clone 仓库，再把目录安装到对应的 skills 目录。

### 方式二：手动安装

```bash
git clone git@github.com:JuneYaooo/nihaixia.git
cd nihaixia
bash install_as_skill.sh --target codex    # Codex
# 或
bash install_as_skill.sh --target claude   # Claude Code
```

脚本会把 skill 装到：

- Codex: `~/.codex/skills/nihaixia/`
- Claude Code: `~/.claude/skills/nihaixia/`
- OpenClaw: `~/skills/nihaixia/`

装完后重启对应 agent，让 skill 元数据重新加载。

## 使用示例

```text
用 nihaixia 帮我整理太阳中风和太阳伤寒的区别。
```

```text
用 nihaixia 查桂枝汤、麻黄汤、葛根汤的方证分水岭。
```

```text
用 nihaixia 按白话解释：为什么有的人感冒怕冷无汗，有的人怕风有汗？
```

```text
用 nihaixia 找小柴胡汤相关的板书截图证据。
```

截图检索也可以直接跑脚本：

```bash
python3 scripts/search_screenshots.py 小柴胡汤 加减
python3 scripts/search_screenshots.py 少阴 下利
```

> 截图索引会返回原始整理环境中的截图路径。没有本地课程截图文件时，仍可使用时间点、课次和截图描述做资料定位；有同名 `media_lessons_distill` 工作区时可直接打开原图。

## 安全说明

本项目用于倪海厦课程学习、资料检索和中医理论整理，不用于医疗诊断或个体化治疗。

涉及附子类、四逆汤辈、大承气汤/急下存阴、抵当汤、大陷胸汤、癌症/肿瘤、妊娠、儿童、胸痛、意识改变、严重脱水或其他急危重症时，应立即咨询合格医生或急诊处理。

## 当前覆盖

- 已整理：`07.伤寒论课程`
- 待扩展：`金匮要略`、`针灸大成/人纪针灸`、`黄帝内经`、`神农本草经`
