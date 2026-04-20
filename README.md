# Frontend Slides · Claude Code Skill

为 [Claude Code](https://code.claude.com) 打造的 HTML 演示 PPT 生成 skill。

✨ 核心能力：
- **零依赖**：单个 HTML 文件即可运行
- **12 种风格预设**：从 Paper & Ink 到 Neon Cyber
- **电影级模式**：支持视频背景、玻璃拟态、胶片颗粒、逐字动画
- **一页一屏**：视口严格适配，不滚动

## 安装

### 方法一：Git Clone（推荐）

```bash
mkdir -p ~/.claude/skills/
git clone https://github.com/Harrisonford-ss/claude-skill-frontend-slides.git ~/.claude/skills/frontend-slides
```

### 方法二：下载 tarball

```bash
mkdir -p ~/.claude/skills/
curl -L https://github.com/Harrisonford-ss/claude-skill-frontend-slides/archive/refs/heads/main.tar.gz | tar -xz -C /tmp/
mv /tmp/claude-skill-frontend-slides-main ~/.claude/skills/frontend-slides
```

## 使用

装好后**重启 Claude Code**，然后对 Claude 说：

```
帮我做一个分享 PPT
```

或使用斜杠命令：

```
/frontend-slides
```

## 包含文件

| 文件 | 用途 |
|------|------|
| `SKILL.md` | Skill 主入口，Claude 会读这个文件激活能力 |
| `STYLE_PRESETS.md` | 12 种风格预设 + 强制性视口适配 CSS |
| `CINEMATIC_CASE_STUDY.md` | 🎬 电影级模式实战案例（视频背景 + 玻璃卡 + 胶片颗粒） |

## Cinematic 电影级模式

当演讲需要"Apple 发布会级别"的视觉感时触发。核心技术栈：

1. 视频做 hero 背景（brightness/saturate/contrast 滤镜）
2. 多层渐变遮罩（文字区压暗 + 氛围色漏光）
3. SVG 噪点贴图 = 胶片颗粒（零网络依赖）
4. 扫描线 mix-blend-mode: overlay（低透明度潜意识效果）
5. Glassmorphism 数据卡（blur + saturate(180%) + 顶部高光线）
6. 取景框角标（4 个 L 形角标）
7. CJK + Latin 双字体系统（思源宋体 900 + Inter 100）
8. 逐字入场动画（最后两字带发光色彩）

源自「夷陵之火」AI 短剧生产线演讲分享 PPT 的实战总结。

## 作者

由 Eliza · 郑懿洋 维护。

Skill 基础框架来自 [ECC (Everything Claude Code)](https://github.com/) 社区。
Cinematic 案例由 Eliza 原创贡献。

## 许可

MIT
