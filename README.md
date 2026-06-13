# MarxChou Illustrations

> 把中文技术文章里的判断、流程、状态和隐喻，变成一张张白底、手绘、清爽的正文配图。
>
> 16:9 横版 | MarxChou IP | 纯白手绘 | 少量红橙蓝中文批注 | 适配 Hermes Agent & Codex

Forked from [Ian Xiaohei Illustrations](https://github.com/helloianneo/ian-xiaohei-illustrations) by [Ian](https://www.ianneo.xyz).

---

## 这个仓库是什么

MarxChou Illustrations 是一个 AI Agent Skill，用来指导 AI 为中文技术博客文章生成正文配图。

它不是通用插画 prompt，也不是 PPT 信息图模板。它的核心目标是：先理解文章里的认知锚点，再把其中一个判断、流程、结构、状态或隐喻，变成一张有记忆点的 16:9 手绘解释图。

默认视觉 IP 是 MarxChou：蓬松短发轮廓、圆框眼镜、青绿色卫衣（黑线手绘 + 手写 "M" 标记）、冷静认真的表情。MarxChou 不是吉祥物，不是贴纸，也不是站在角落里的装饰物，而是正在认真参与系统运转的独立开发者。

一句话：**让 AI 不只是「配一张图」，而是把文章里的一个关键认知动作画出来。**

---

## 适合谁用

特别适合：

- 写中文技术博客，需要正文配图和文章插图的人
- 做独立开发、NAS、Linux、Docker、自建服务相关内容的人
- 想把抽象判断画成具体隐喻的人
- 想要一种比 PPT 信息图更轻、更怪、更有个人识别度的配图风格的人
- 用 AI Agent 做内容生产，希望稳定复用一套视觉语言的人

不适合：

- 想要商业插画、品牌 KV 或精致扁平插画的人
- 想要传统 PPT 信息图、复杂架构图或流程图的人
- 想要儿童卡通、可爱 IP、表情包风格的人
- 想把大量正文、长段解释或完整课程页塞进一张图里的人

---

## 视觉风格

- 纯白背景，不要纸纹、米色、阴影、渐变
- 黑色手绘线稿，细线，轻微抖动
- 大量留白，主体只占画面约 40%-60%
- 少量红色、橙色、蓝色中文手写批注
- 一张图只表达一个核心动作、结构、状态或隐喻
- MarxChou 必须参与核心动作，不能只是装饰
- 有创意、清爽，但不幼稚、不卖萌、不像 PPT

---

## 安装

克隆仓库：

```bash
git clone https://github.com/Smart-Chou/xiaohei-illustrations.git
```

### Hermes Agent

复制到 Hermes skills 目录：

```bash
cp -R ./ian-xiaohei-illustrations ~/.hermes/skills/creative/xiaohei-illustrations/
```

使用 `/skill xiaohei-illustrations` 加载。

### Codex

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R ./ian-xiaohei-illustrations "${CODEX_HOME:-$HOME/.codex}/skills/"
```

---

## 怎么用

### 只做配图规划

```text
Use xiaohei-illustrations 先不要生图。
请分析下面这篇文章哪里值得配图，输出 5 张左右的 shot list。
每张图写清楚：放在哪段后、主题、核心意思、结构类型、MarxChou 在做什么、建议中文标注词。

<粘贴文章>
```

### 直接生成正文配图

```text
Use xiaohei-illustrations 把下面这篇文章生成 4 张手绘正文配图。
要求：16:9 横版、纯白背景、黑色手绘线稿、少量红橙蓝中文手写批注。

<粘贴文章>
```

### 为单个概念生成一张图

```text
Use xiaohei-illustrations 为「信任不是喊出来的，而是一块证据一块证据铺过去」生成一张正文配图。
画面要怪诞但清爽，MarxChou 必须承担核心动作。
```

---

## 工作流程

1. 读取文章、Markdown 内容或用户给的主题
2. 提炼核心观点、认知转折、流程结构和适合视觉化的段落
3. 先输出 shot list：每张图只选一个认知锚点
4. 为每张图选择结构类型：Workflow、系统局部、前后对比、角色状态、概念隐喻、方法分层、地图路线或小漫画分镜
5. 重新发明一个低科技、怪诞但成立的物理隐喻
6. 让 MarxChou 承担核心动作
7. 每张图单独调用图像模型生成
8. 按 QA checklist 检查：白底、留白、MarxChou 动作、中文标注、非 PPT 感、非旧案例复刻
9. 保存最终 PNG，并报告用途和路径

---

## 目录结构

```text
.
├── README.md
├── LICENSE
├── NOTICE.md
├── examples/
│   ├── images/
│   │   ├── 01-two-breakpoints.png
│   │   └── ...
│   └── prompts.md
└── ian-xiaohei-illustrations/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    ├── assets/
    │   └── examples/
    └── references/
        ├── style-dna.md
        ├── xiaohei-ip.md
        ├── composition-patterns.md
        ├── prompt-template.md
        └── qa-checklist.md
```

---

## 注意事项

- 图片里的中文文字越短越稳定。
- 每张图只讲一个核心结构，不要把文章做成说明书。
- MarxChou 必须承担核心动作；如果去掉 MarxChou 画面仍然完全成立，说明他太装饰了。
- 示例图只用于校准线条密度、留白、颜色克制和 MarxChou 参与方式，不要复刻构图。
- AI 图像模型可能出现错字、幻觉标签、风格漂移或多余标题，生成后需要检查。
- 如果中文错字严重，优先减少标注词并重生成。

---

## 关于

Forked from [Ian Xiaohei Illustrations](https://github.com/helloianneo/ian-xiaohei-illustrations) by [Ian (伊恩)](https://www.ianneo.xyz).

MarxChou 适配版由 [MarxChou](https://marxchou.com) 维护。

---

## License

MIT License. See [LICENSE](LICENSE).
