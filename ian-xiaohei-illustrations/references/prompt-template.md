# 生图提示词模板

每张图单独生成。根据正文内容替换变量，不要把多张图拼在一起。

```text
Generate one standalone 16:9 horizontal Chinese article illustration.

Style:
手绘铅笔素描风，简约干净线稿，纯色空白背景，线条粗细一致，写实轻漫画质感。大量留白。少量红色/橙色/蓝色中文手写批注。禁止PPT、信息图、商业插画、复杂背景、阴影、渐变、纸纹。

MarxChou character (must appear, must perform core action):
同一个清瘦少年男生，蓬松凌乱短发，黑细圆框眼镜，身穿固定青绿色连帽卫衣，卫衣胸口有黑色大写M字母，身形比例统一，五官柔和沉稳，表情安静专注。仅卫衣填充统一青绿色，其余人物全黑白线条。人物五官脸型完全复刻基准形象，不改变长相发型服饰。

Negative prompt:
Q版，大头娃娃，厚涂油画，水彩浓彩，染发，换外套，无眼镜，脸型变形，五官偏移，夸张表情，肥胖身材，多人，杂乱背景，阴影过重，色彩杂乱，chibi，cartoon，cute，child

Theme:
{正文配图主题}

Structure type:
{结构类型：Workflow / 系统局部 / 前后对比 / 角色状态 / 概念隐喻 / 方法分层 / 地图路线 / 小漫画分镜}

Core idea:
{这张图要表达的核心意思}

Composition:
{具体画面：MarxChou 在哪里、正在做什么、主要物件是什么、信息如何流动}

Suggested elements:
{元素1} / {元素2} / {元素3} / {元素4}

Chinese handwritten labels:
{标注词1} / {标注词2} / {标注词3} / {标注词4} / {可选标注词5}

Color rules:
MarxChou 仅卫衣填青绿色，其余全黑白线条。标注用红色（重点/问题/提醒）、橙色（主流程/箭头/路径）、蓝色（补充说明/系统状态）。

Constraints:
一张图只讲一个核心结构。主体占画面 40%-60%。至少 35% 留白。最多 5-8 个短中文标注。左上角不写标题。不要写结构类型名称。不要做成正式流程图/课件/说明书。不要复刻旧案例构图——每次从当前文章重新发明隐喻。画面要清爽、有意思、简洁，不幼稚不死板。
```

## 图像编辑提示

去掉左上角标题：

```text
Edit the provided image. Remove only the handwritten title "{要删除的文字}" and its underline from the top-left corner. Fill that area with the same clean white background, matching the surrounding blank paper. Preserve everything else exactly: characters, labels, paths, line style, composition, aspect ratio, and image quality. Do not add any new text or objects.
```

增强画面感：

```text
Regenerate this illustration with the same core meaning and simple layout, but make MarxChou more central to the conceptual action. MarxChou should be doing the work that explains the idea, not standing beside the diagram. Keep the pencil sketch style, clean line art, teal hoodie only colored, pure white background, sparse annotations.
```
