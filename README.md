# Liquid AI Cockpit (液态智能驾驶舱)

> 基于 [LiquidGlass-UI](https://github.com/idhdi/LiquidGlass-UI) 物理光学引擎打造的下一代 AI 交互与监控驾驶舱插件。

## 🌟 核心特性

- 💧 **水滴粘滞思考态 (Gooey Thinking Pulse)**：利用 SVG 高斯模糊 + 颜色矩阵阈值化，模拟真实液体表面张力的拉丝断裂与融合回弹。
- 🌈 **动态菲涅尔边缘光 (Fresnel Rim Light)**：根据鼠标移动实时计算光束焦点，倒角边缘聚光反射。
- 🧊 **3D 玻璃物理厚度视差 (3D Depth & Parallax)**：透视倾斜配合三层空间深度位移，呈现 5mm 水晶玻璃厚重感。
- 🌊 **水下波光焦散层 (Caustics Drift Layer)**：深邃多层渐变漂移，流光溢彩。
- 🔍 **代码微观折射透镜 (Optical Lens Inspector)**：置换贴图驱动的物理级局部放大与 RGB 棱镜色散。
- 💧 **水珠重力流淌 (Trickle & Wet Trail)**：凝结水珠受重力滑落，留下渐隐湿痕。

## 📁 目录结构

```text
liquid-ai-hud/
├── plugin.json                 # Antigravity 插件配置元信息
├── sidecars/
│   └── liquid_hud/
│       ├── sidecar.json        # 注册侧边栏辅助面板 (Auxiliary Pane)
│       ├── server.mjs          # 本地微服务 (Node.js)
│       └── web/
│           └── index.html      # 驾驶舱主界面 (纯原生 Web Components + CSS)
└── README.md
```

## 🚀 启动与使用

在 Antigravity 中安装为插件，或在本地启动开发预览：

```bash
cd sidecars/liquid_hud
node server.mjs
# 打开 http://127.0.0.1:4173 即可预览
```
