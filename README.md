# Douyin Chat Bubble Skill · 抖音聊天气泡设计 Skill

[English](README.en.md)

利用 Codex 设计抖音 IM 点九图聊天气泡、改图并做上传前检查的 skill。

它把两类约束放在一起：抖音静态资源尺寸、文本和边距要求，以及本项目额外要求的点九拉伸安全结构。独立维护和更新，不必跟随任何其他项目一起升级。

<p align="center">
  <a href="https://github.com/kaitongg-bit/douyinQIPAO"><img src="https://img.shields.io/github/stars/kaitongg-bit/douyinQIPAO" alt="Stars"></a>
  <img src="https://img.shields.io/badge/license-MIT-blue" alt="MIT">
</p>

## 包含内容

- `SKILL.md`：设计与交付流程；包含镜像安全、文字区和点九图结构规则。
- `references/douyin-rules.md`：平台要求及本地体验约束的摘要。
- `references/pixel-preflight.md`：边距与锚点检查的说明。
- `scripts/edge_spacing.py`：透明 PNG 的确定性预检工具。

## 最重要的拉伸规则

每个气泡都要在设计开始前声明一个可拉伸的锚点矩形 `left, top, right, bottom`。它的上、下、左、右四条边都必须是连续的直线。角色、肉垫、弧线、透明缺口和纹理都不能替代这四条边。

即使是无框、手绘或异形设计，也应以低对比度的平直底面保留锚点；所有有辨识度的细节放入固定角区。

## 检查 PNG

安装依赖：

```bash
python3 -m pip install Pillow
```

检查画布、平台式边距和四边锚点：

```bash
python3 scripts/edge_spacing.py bubble.png --anchor-rect 47 32 174 126
```

只有输出同时包含以下两项时，才适合进入上传预览：

```text
ANCHORS: PASS
OVERALL: PASS
```

脚本不取代抖音最终上传预览；仍需在平台内设置文字区域和分割线，并测试短消息、长单行、多行消息以及深浅模式。

## 本地安装为 Codex skill

将这个仓库文件夹放到 `~/.codex/skills/douyin-chat-bubble/` 后重启或刷新技能列表即可。

## 许可证

本项目代码与文档采用 [MIT License](LICENSE)，可自由使用、修改和分发（包括商用）。

未附带第三方气泡素材或生成图片；素材授权问题与本项目许可证无关。使用者需确保自己的角色、素材和最终上传内容具备相应授权。
