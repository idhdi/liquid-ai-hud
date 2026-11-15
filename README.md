# Liquid AI Cockpit (液态智能驾驶舱)

> 基于 [LiquidGlass-UI](https://github.com/idhdi/LiquidGlass-UI) 物理光学引擎打造的 AI 交互与监控驾驶舱插件，以 **Antigravity Auxiliary Pane** 侧栏形式运行。

## 🌟 核心特性

- 💧 **水滴粘滞思考态 (Gooey Thinking Pulse)**：SVG 高斯模糊 + 颜色矩阵阈值化，模拟液体表面张力的拉丝断裂与融合回弹。
- 🌈 **动态菲涅尔边缘光 (Fresnel Rim Light)**：根据鼠标位置实时计算光束焦点，倒角边缘聚光反射。
- 🧊 **3D 玻璃物理厚度视差 (3D Depth & Parallax)**：透视倾斜配合三层空间深度位移，呈现 5mm 水晶玻璃厚重感。
- 🌊 **水下波光焦散层 (Caustics Drift Layer)**：多层渐变漂移，流光溢彩。
- 🔍 **代码微观折射透镜 (Optical Lens Inspector)**：置换贴图驱动的局部放大与 RGB 棱镜色散。
- 💧 **水珠重力流淌 (Trickle & Wet Trail)**：凝结水珠受重力滑落，留下渐隐湿痕。
- 🧩 **Aux Pane 窄宽度适配 / 减少动画偏好**：560px 以下自动切换为紧凑布局，`prefers-reduced-motion` 下停用持续动画。

> 说明：当前界面中的 AI 状态、吞吐、Subagent 等数据为**前端模拟演示**，尚未接入真实模型 / Agent 流。插件骨架、侧栏能力与光学材质已就绪，可按需接入 Antigravity SDK 或自有后端。

## 📁 目录结构

```text
liquid-ai-hud/
├── plugin.json                 # Antigravity 插件清单（$schema / logo / 元信息）
├── assets/
│   └── logo.svg                # 插件图标
├── sidecars/
│   └── liquid_hud/
│       ├── sidecar.json        # 注册 Aux Pane 侧栏视图
│       ├── server.mjs          # 本地静态服务（Node.js，127.0.0.1）
│       └── web/
│           └── index.html      # 驾驶舱主界面（单文件、零外部依赖）
├── README.md
└── LICENSE
```

## 🚀 安装

插件遵循 Antigravity 官方插件结构：`plugin.json` + `sidecars/<id>/`（参考 [Plugins](https://antigravity.google/docs/plugins/) 与 [Sidecars](https://antigravity.google/docs/sidecars/) 文档）。

### 方式一：本地目录安装（推荐）

1. 将本仓库放到插件目录：

   ```text
   全局：~/.gemini/config/plugins/liquid-ai-hud/
   或工作区：<project>/.agents/plugins/liquid-ai-hud/
   ```

2. 在 Antigravity 中打开 `/plugin`，在 Installed 里启用 **Liquid AI Cockpit**；或直接编辑 `~/.gemini/config/config.json` 启用 `sidecars["liquid-ai-hud/liquid_hud"]`。
3. 在 Auxiliary Pane 的 `+` 菜单选择 **Liquid AI HUD**。

### 方式二：开发预览（不装插件）

```bash
cd sidecars/liquid_hud
node server.mjs
# 打开 http://127.0.0.1:4173
```

指定端口（Antigravity 运行时会自动注入 `PORT`）：

```powershell
$env:PORT=4200; node server.mjs
```

```bash
PORT=4200 node server.mjs
```

## 🔒 服务端行为

`server.mjs` 只监听 `127.0.0.1`，并做了以下约束：

- 使用 `new URL(req.url)` 取 pathname，查询串不会再导致 404；
- `path.resolve` + 前缀校验，`/../server.mjs` 等路径穿越请求返回 `403`；
- 仅允许 `GET/HEAD`，其余返回 `405`；
- 完整 MIME 映射（html/js/css/svg/png/woff2…）、`Content-Length`、`no-store`、`nosniff`；
- 支持 `PORT` 环境变量与优雅退出，便于 Antigravity 重启 sidecar。

## 🧪 本地验证

```bash
node --check sidecars/liquid_hud/server.mjs
PORT=4201 node sidecars/liquid_hud/server.mjs &
curl -I http://127.0.0.1:4201/                 # 200
curl -I "http://127.0.0.1:4201/?cache=1"       # 200（查询串不再 404）
curl -I --path-as-is http://127.0.0.1:4201/../server.mjs   # 403
```

## 📄 License

MIT
