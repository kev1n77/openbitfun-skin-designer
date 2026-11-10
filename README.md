# OpenBitFun Skin Designer

An Agent skill for creating and updating importable OpenBitFun visual skins from reference images or an art brief.

用于根据参考图或文字要求设计 OpenBitFun 视觉皮肤，交付可编辑的 `skin.json`、本地素材和可导入的 ZIP。技能入口为 [SKILL.md](SKILL.md)。

## 设计方式

- 从目标 OpenBitFun 源码导出当前真实契约，使用已开放的颜色、阴影、区域、组件部件和交互状态。
- 支持纯配色、局部材质和连续背景等设计方向；内置 Aurora Paper 仅作语法示例。
- 复用产品正式解析器校验和打包，独立检查真实产品中的视觉效果。
- 保持产品的布局、尺寸、圆角、排版和交互行为；不注入 CSS、JavaScript 或 HTML。

## 使用

将本仓库作为支持 `SKILL.md` 的 Agent 技能目录加载，然后调用 `openbitfun-skin-designer`，提供参考图或设计要求、目标 OpenBitFun 项目路径、需要的明暗模式和页面范围。

辅助脚本需要：

- Node.js 22.12 或更新版本。
- 包含视觉皮肤系统的 OpenBitFun 源码，以及通过 `pnpm install` 安装的项目依赖。
- 已准备好的设计系统包；必要时在目标项目执行 `pnpm --dir src/web-ui run prepare:design-system:dev`。

技能可以独立安装；辅助脚本仍需要目标源码来读取当前能力和运行产品校验器。它不会自动下载产品源码、安装或启用皮肤。

```text
node /path/to/openbitfun-skin-designer/scripts/visual-skin.mjs contract --project /path/to/OpenBitFun
node /path/to/openbitfun-skin-designer/scripts/visual-skin.mjs init /path/to/new-skin --id my-skin --name "My Skin" --project /path/to/OpenBitFun
node /path/to/openbitfun-skin-designer/scripts/visual-skin.mjs validate /path/to/new-skin --project /path/to/OpenBitFun
node /path/to/openbitfun-skin-designer/scripts/visual-skin.mjs pack /path/to/new-skin --out /path/to/my-skin.zip --project /path/to/OpenBitFun
node /path/to/openbitfun-skin-designer/scripts/visual-skin.mjs validate /path/to/my-skin.zip --project /path/to/OpenBitFun
```

路径有空格时请加引号；`init` 目录和 `pack` 输出文件必须尚不存在。

校验通过只表示结构合规。脚本始终将视觉验收标为 `draft-unverified`；需要结合真实产品截图、控件状态和可读性检查完成验收。

## 目录

| 路径 | 内容 |
| --- | --- |
| [SKILL.md](SKILL.md) | Agent 工作入口与交付要求 |
| [references/contract.md](references/contract.md) | 皮肤导入契约与能力边界 |
| [references/paint-owners.md](references/paint-owners.md) | 产品组件和绘制部位说明 |
| [references/authoring-template.md](references/authoring-template.md) | 可选创作方法 |
| [references/visual-review.md](references/visual-review.md) | 实际产品视觉检查 |
| `references/templates/` | 可选设计与验收工作表，不进入皮肤 ZIP |
| `examples/aurora-paper/` | 可编辑语法示例 |
| `scripts/` | 契约导出、初始化、校验、打包及测试 |

## 测试

在已安装依赖的目标 OpenBitFun 源码目录中执行，脚本路径指向本仓库：

```text
node --test /path/to/openbitfun-skin-designer/scripts/visual-skin.test.mjs
```

测试覆盖正式解析器、打包、资源边界和创作检查，不代替原生界面验收。

## 来源与许可

从 [OpenBitFun](https://github.com/GCWing/OpenBitFun) 的内置视觉皮肤 Skill 提取，原名 `create-visual-theme`，现名 `openbitfun-skin-designer`。

沿用上游 [MIT License](LICENSE)，保留原版权声明。
