# 国漫打斗提示词引擎 · Guoman Fight Prompt Engine

> 把两则顶级 **3D 次世代国漫打斗提示词**蒸馏成一套**可套用于任何打斗**的六层装配引擎。
> A distilled, reusable prompt-engineering skill for **3D next-gen Chinese-animation style fight scenes**.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Skill](https://img.shields.io/badge/type-Agent%20Skill-blue.svg)](./SKILL.md)

---

## 这是什么

两则优质提示词（骨伞女 × 剑女 / 黑发剑客 × 骨伞女）里藏着同一套语法。本项目把它拆出来、参数化，做成一个 Agent Skill：

**输入**「谁和谁、在哪、用什么招」 → **输出**「可直接出片的 3D 次世代国漫动作提示词」。

不复刻那两个具体场景，只保留它们的**引擎**：

| 层 | 名称 | 作用 |
|---|---|---|
| L1 | 技术锚定层 | 8K 3D CG 写实 + PBR + 院线电影级色彩分级 + 超写实微观清单 |
| L2 | 战场层 | 高落差 + 可破坏物 + 天气光源 |
| L3 | 角色层 | 双人对撞：每人一个「色 + 物性 + 运动方式」的**附着型**气场 |
| L4 | 特效语法层 | **三级碰撞固定特效矩阵**（轻 / 重 / 大招） |
| L5 | 运镜物理层 | 3A 惯性追尾机位；零站桩 / 无匀速 / 无对波；位移双量化 |
| L6 | 分镜节奏层 | 12 镜功能位曲线，东方残心收势 |

## 核心资产：三级碰撞矩阵

风格里唯一被写成「强制匹配」的接口。每次碰撞先判等级，再挂载固定组件：

| 等级 | 组件 | 抽帧 | 频次 |
|---|---|---|---|
| **轻碰撞** | 冲击帧 + 局部负片 + 轴向微甩 + 粒子飞溅 | 0.05s | 高 |
| **重碰撞** | 放射冲击帧 + 中心负片 + 受力猛沉/回弹 + 三层粒子爆炸 | 0.10s | 中 |
| **大招爆发** | 全屏冲击帧 + 全屏负片闪白 + 径向剧烈震动 + 中心鱼眼畸变 + 环形冲击波 | 0.15s | 全片 1–2 次 |

**不可替换的组件**：负片、抽帧、鱼眼畸变、径向震荡、泛光、环形冲击波 —— 这些是电影语法，与题材无关。

## 12 镜节奏母版

```
静 → 脸 → 重击 → 拆招 → 升格 → 爆气 → 异象 → 大招 → 留白 → 爆发 → 残心 → 爆碎
 1     2     3      4      5      6      7      8      9      10     11     12
```

两个**必须存在的低谷**：镜头 1（开场静）与镜头 9（大招前 0.5s 留白）。没有低谷，高潮就不值钱。

## 题材位移：换皮不换骨

骨架与三级碰撞在任何题材下逐字保留，只换材质语义：

| 题材 | 特效材质 | 拖尾 | 破坏物 |
|---|---|---|---|
| 古武/武侠 | 雾山五行水墨飞白 | 水墨残影 | 石柱、木栏、铜钟 |
| 仙侠/玄幻 | 罡气 + 符箓 | 灵光拖尾 | 断桥、经幡、山岩 |
| 现代/都市 | 水花 + 玻璃碎屑 | 水痕烟尘 | 玻璃幕墙、汽车 |
| 科幻/机甲 | 等离子环 + 电弧网 | 光轨离子尾 | 舱壁、装甲板 |
| 赛博朋克 | 全息残影 + 数据流 | 像素化残影 | 全息牌、管线、贩卖机 |
| 校园/日常 | 雨水 + 尘粒 | 水花汗滴 | 课桌、储物柜、篮球架 |

## 目录结构

```
.
├── SKILL.md                      # 主引擎：六层模型 + 工作流 + QA 清单
├── references/
│   ├── 01-style-dna.md           # 两则原始提示词的 DNA 对照拆解
│   ├── 02-collision-vfx.md       # 三级碰撞矩阵、抽帧时间表、技法名词表
│   ├── 03-camera-motion.md       # 运镜术语库（中英）、机位体系、位移量化写法
│   ├── 04-move-lexicon.md        # 招式词库、气场形容词库、色彩对撞配色表
│   ├── 05-shot-rhythm.md         # 12 镜节奏曲线与每镜功能
│   └── 06-genre-shift.md         # 题材风格位移表
├── templates/
│   ├── intake-form.md            # 输入采集槽位表
│   └── fight-prompt-template.md  # 可填空成品模板（版式 A / B）
└── examples/
    ├── example-01-original-sample-a.md     # 原始样本 A + 结构标注
    ├── example-02-original-sample-b.md     # 原始样本 B + 结构标注
    ├── example-03-cyber-rain-duel.md       # 【跨题材验证】赛博朋克·霓虹雨夜·12 镜
    ├── example-04-modern-garage-brawl.md   # 【跨题材验证】现代车库·徒手格斗·10 镜
    └── raw/                                # 两则原始提示词原文归档
```

## 安装

### WorkBuddy / Claude Code 风格 Agent Skill

把整个仓库克隆到 skills 目录即可：

```bash
git clone https://github.com/yimao1234/guoman-fight-prompt.git \
  ~/.workbuddy/skills/guoman-fight-prompt
```

Windows：

```powershell
git clone https://github.com/yimao1234/guoman-fight-prompt.git `
  "$env:USERPROFILE\.workbuddy\skills\guoman-fight-prompt"
```

装好后，直接说「写一场 XX 风格打斗」即可触发。

### 当作纯提示词模板用

不需要 Agent 也可以：打开 `templates/fight-prompt-template.md`，按填空说明逐段填，再对照 `SKILL.md` 的 QA 清单自检。

## 快速上手

**输入**：

> 写一场赛博朋克风的打斗，义体刀客对上重装机甲

**引擎输出**：见 [`examples/example-03-cyber-rain-duel.md`](./examples/example-03-cyber-rain-duel.md) —— 12 镜完整成品，含三级碰撞、升格击飞、留白、残心入鞘与延迟爆碎。

## 九条硬性红线

1. 零站桩
2. 无匀速影视慢推拉
3. 无隔空对波（永远近身实体碰撞）
4. 无悬浮光污染（特效必须附着）
5. 重击必击飞，击飞必追击
6. 气场不得均匀（须随动作强度动态变化）
7. 人物占画面 ≥ 1/3（禁止把人拍成空镜里的黑点）
8. 大招前必有 0.3–0.5s 留白
9. 结尾声明：无 BGM、无字幕、无水印，纯画面输出

## English Summary

This skill distills two high-quality **3D next-gen Chinese-animation (guoman) fight-scene prompts** into a parameterized six-layer assembly engine. It does not reproduce those two scenes — it extracts their grammar: a **three-tier collision VFX matrix** (light / heavy / ultimate), a **12-shot rhythm curve**, a **game-like chase-camera doctrine** (zero standing still, no uniform dolly, no ranged energy duels, every displacement quantified in seconds and screen ratio), and an **Eastern "residual-heart" ending** (sheathing, then a delayed destruction beat).

Swap the material semantics (ink-wash → plasma → rain spray → pixel artifacts) and the same skeleton works for wuxia, xianxia, modern urban, sci-fi mecha, cyberpunk, or campus fights.

## License

[MIT](./LICENSE)

原始两则提示词仅作风格分析归档，版权归原作者所有（见 `examples/raw/`）。
