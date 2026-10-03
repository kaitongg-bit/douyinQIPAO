# Douyin Chat Bubble Skill

[中文](README.md)

A Codex skill for designing Douyin IM nine-slice chat bubbles, editing images, and pre-upload checking.

It combines two kinds of constraints: Douyin's static-asset size, text, and margin requirements, plus the nine-slice stretch-safe structure this project additionally requires. It is maintained and updated independently and does not move in lockstep with any other project.

<p align="center">
  <a href="https://github.com/kaitongg-bit/douyinQIPAO"><img src="https://img.shields.io/github/stars/kaitongg-bit/douyinQIPAO" alt="Stars"></a>
  <img src="https://img.shields.io/badge/license-MIT-blue" alt="MIT">
</p>

## What's inside

- `SKILL.md`: the design and delivery flow, including mirror-safety, text-area, and nine-slice structure rules.
- `references/douyin-rules.md`: a summary of platform requirements and local experience constraints.
- `references/pixel-preflight.md`: notes on margin and anchor checks.
- `scripts/edge_spacing.py`: a deterministic preflight tool for transparent PNGs.

## The one stretch rule that matters

Every bubble must declare a stretchable anchor rectangle `left, top, right, bottom` before design starts. All four edges must be continuous straight lines. Characters, paw pads, curves, transparent gaps, and textures cannot stand in for these edges.

Even borderless, hand-drawn, or irregular designs should keep their anchors as a low-contrast flat base; put all recognizable details in the fixed corner areas.

## Checking a PNG

Install the dependency:

```bash
python3 -m pip install Pillow
```

Check the canvas, platform-style margins, and the four anchor edges:

```bash
python3 scripts/edge_spacing.py bubble.png --anchor-rect 47 32 174 126
```

The image is ready for upload preview only when the output contains both of these:

```text
ANCHORS: PASS
OVERALL: PASS
```

The script does not replace Douyin's final upload preview; you still need to set the text area and divider lines in the platform, and test short messages, long single lines, multi-line messages, and light/dark modes.

## Installing as a local Codex skill

Put this repository folder at `~/.codex/skills/douyin-chat-bubble/`, then restart or refresh the skill list.

## License

The code and documentation in this project are released under the [MIT License](LICENSE) — free to use, modify, and distribute, including commercially.

No third-party bubble assets or generated images are bundled; asset licensing is separate from this project's license. Users are responsible for ensuring their characters, assets, and final uploads have the necessary authorization.
