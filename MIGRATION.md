# MarxChou 插图 Skill 改造实录

> 从 Ian 的「小黑怪诞手绘」到 MarxChou 的「铅笔素描技术配图」——一次完整的 AI 插图风格迁移记录。

---

## 背景

原项目 [Ian Xiaohei Illustrations](https://github.com/helloianneo/ian-xiaohei-illustrations) 是一套为中文文章生成正文配图的 AI Agent Skill，默认 IP 是「小黑」——一个黑色实心 blob 小怪物，风格为白底黑线手绘 + 少量红橙蓝中文批注。

我需要把这个 Skill 适配到自己的个人 IP **MarxChou**：清瘦少年、蓬松短发、黑细圆框眼镜、青绿色连帽卫衣（胸口黑色 M 字母）。

---

## 过程

### 第一阶段：IP 形象设计

先用 AI 生成了 MarxChou 的完整品牌 IP 设计稿：
- 卡通风（chibi）：彩色 3D Pixar 风格
- 像素风（16-bit SNES）：复古游戏风格
- 最终选定：铅笔素描风，清瘦少年，仅卫衣填青绿，其余全黑白

### 第二阶段：生成后端选型

Hermes Agent 内置 `image_generate` 工具，需配置后端：

1. 默认后端 FAL 没有 API Key，不可用
2. 已有火山方舟 ARK API Key（vision 模型在用）
3. 火山方舟插件已安装但未选中——需在 `config.yaml` 显式配置：

```yaml
image_gen:
  provider: volcengine
```

4. 模型：`doubao-seedream-5-0-260128`（Seedream 5.0 Lite）

### 第三阶段：风格探索（走了弯路）

#### 尝试 1：保留小黑风格，替换角色
- 用 Seedream 生成「手绘白板草图 + 简笔 MarxChou」
- 结果：可行，但风格太像原版

#### 尝试 2：改为像素风
- 生成 16-bit SNES 像素 MarxChou
- 效果不错，但对中文标注支持差、不够灵活

#### 尝试 3：改为 chibi 矢量风
- 生成精致 3D Pixar 风 MarxChou
- 效果最好看，但用户觉得「太像产品宣传图，不像正文配图」

#### 最终方案：铅笔素描风
- 用户给出了精确的中文提示词模板
- 铅笔素描 + 清瘦少年 + 仅卫衣填色 + 纯白背景

### 第四阶段：两个关键问题

#### 问题 1：人物比例漂移（chibi 大头）

**现象**：部分图 MarxChou 是正常成人比例，部分图变成 chibi 大头娃娃。

**根因**：Seedream 对「手绘草图/doodle/sketch」这些词会触发 chibi 卡通模式，加再多 age constraint 都压不住。

**尝试过的修法**：
- 改英文描述为「editorial illustration, New Yorker style」→ 部分改善
- 加强负面词「NOT chibi, NOT child」→ 无效
- 换 Seedream 4.5 → 模型不存在（404）

**最终解决**：用户给出了完整的中文人物描述，用「铅笔素描风 + 写实轻漫画质感 + 清瘦少年 + 身形比例统一」+ 负面词「Q版，大头娃娃」，一步到位。

#### 问题 2：画面出现杂乱线条

**现象**：图上有与场景无关的红色/橙色涂鸦线和多余标注。

**根因**：风格描述中的「少量红色/橙色中文手写批注」被 Seedream 理解为「到处撒点红橙色涂鸦」。

**解决**：去掉通用批注描述，改为「极度简洁，画面中只出现下述指定的元素」，每个标签在场景描述中逐一指定。

### 第五阶段：逐张审批重生成

14 张示例图全部用统一 prompt 重生成，用户逐张检查通过。

---

## 最终 Prompt 模板

```
角色（严格锁定）：
同一个清瘦少年男生，蓬松凌乱短发，黑细圆框眼镜，
身穿固定青绿色连帽卫衣，卫衣胸口有黑色大写M字母，
身形比例统一，五官柔和沉稳，表情安静专注。
仅卫衣填充统一青绿色，其余人物、背景全黑白线条。

风格：
手绘铅笔素描风，简约干净线稿，纯色空白背景，
线条粗细一致，写实轻漫画质感。
极度简洁，画面中只出现下述指定的元素，
不要任何多余的线条、涂鸦、装饰或标注。

负面提示词：
Q版，大头娃娃，厚涂油画，水彩浓彩，染发，
换外套，无眼镜，脸型变形，五官偏移，夸张表情，
肥胖身材，多人，杂乱背景，阴影过重，色彩杂乱，
chibi，cartoon，cute，child，杂乱线条，多余线条，
噪点，涂鸦，草稿线，多余的批注
```

---

## 改动文件清单

| 文件 | 改动 |
|------|------|
| `ian-xiaohei-illustrations/SKILL.md` | 核心定位、提示词清单全部改为 MarxChou |
| `references/xiaohei-ip.md` | 角色定义：小黑 blob → MarxChou 铅笔素描 |
| `references/composition-patterns.md` | 全局替换角色名，更新动作池 |
| `references/prompt-template.md` | 完整中文 prompt 模板（含正面+负面） |
| `references/qa-checklist.md` | 新增年龄一致性和画面简洁度检查 |
| `README.md` | 全文中文化，更新为 MarxChou |
| `assets/examples/` (14 张) | 全部重生成 |
| `examples/images/` (8 张) | 全部重生成 |

GitHub 仓库：https://github.com/Smart-Chou/xiaohei-illustrations

---

## 经验教训

1. **Seedream 对风格关键词极度敏感**：「手绘草图」= chibi，「铅笔素描」= 成人比例。一字之差。
2. **中文 prompt 比英文 prompt 更稳定**：中文模型对中文本就更擅长，人物描述用中文比用英文准确得多。
3. **负面 prompt 要穷举**：「Q版」「大头娃娃」「多余线条」一个都不能少。
4. **「少量批注」不要写在风格里**：会被模型理解为随机撒涂鸦。每个标签在场景中逐一指定。
5. **逐张审批比批量生成靠谱**：批量出图容易出现隐蔽问题，逐张看能及时纠偏。
6. **插件加载需要显式配置 provider**：即使插件已 enabled，image_gen 也需要在 config.yaml 里指定 provider 才会被选中。

---

*2026 年 6 月 13 日，MarxChou × Hermes Agent*
