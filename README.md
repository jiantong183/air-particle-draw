# ✨ 隔空粒子手写 · Air Particle Draw

用摄像头识别手势，在空中"捏笔"书写发光粒子笔迹，双手还能缩放镜头。零依赖、单文件、纯前端，开箱即用。

A camera-based **air-writing** web toy: pinch your fingers in the air to draw glowing particle strokes, and use **two hands to zoom**. Single file, zero build step, runs entirely in the browser.

> 灵感来自短视频里的"粒子隔空手写"特效，这是一个独立实现的开源版本。
> Inspired by the "air-writing particle" effects seen in short videos — this is an independent, open-source implementation.

---

## 🎬 在线体验 / Live Demo

部署到 GitHub Pages 后，访问：`https://jiantong183.github.io/air-particle-draw/`

> ⚠️ 摄像头只能在 **HTTPS** 或 **localhost** 下使用。GitHub Pages 是 HTTPS，所以部署后摄像头可直接授权使用；本地直接双击 `index.html`（`file://`）则无法开启摄像头。
> The camera only works over **HTTPS** or **localhost**. GitHub Pages serves HTTPS, so the deployed page works out of the box. Opening the file directly (`file://`) will **not** allow camera access.

---

## 🕹️ 操作 / Controls

| 操作 Action | 手势 / 输入 Gesture / Input |
| --- | --- |
| 落笔 / 抬笔 Pen down / up | 单手 **食指 + 拇指捏合** / 松开 · One hand: **pinch** index + thumb / release |
| 移动笔尖 Move pen | 移动手 / 鼠标 / 手指 · Move hand / mouse / finger |
| 缩放镜头 Zoom | **双手**同时入镜，分开放大、靠拢缩小 · **Two hands**: spread to zoom in, pinch together to zoom out |
| 缩放（桌面）Zoom (desktop) | 鼠标滚轮 · Mouse wheel |
| 复位缩放 Reset zoom | 双击 · Double-click |
| 换颜色 Color | 顶部色块 · Swatches in the top bar |
| 模式 Mode | 底部：书写 / 流光 / 绽放 / 彗尾 · Bottom bar: Write / Trail / Bloom / Comet |
| 清空 Clear | 顶部「清空」按钮 · "Clear" button |

不开摄像头时，可直接用鼠标 / 触摸在屏幕上书写。
Without the camera, you can draw directly with mouse / touch.

---

## 🌟 功能 / Features

- **隔空手势书写** —— 基于 MediaPipe Hands 实时手部追踪，捏合即落笔。
- **平滑笔迹** —— 二次贝塞尔曲线拟合，告别折线感。
- **抑抖滤波** —— One Euro Filter，慢动作强力抑抖、快动作几乎零延迟；捏合判定带迟滞，避免误抬笔。
- **双手缩放镜头** —— 像手机双指缩放；带边缘守卫与每帧限速，抽手不会把缩放带歪。
- **四种特效** —— 书写（持久发光实线）/ 流光 / 绽放 / 彗尾。
- **全屏摄像头背景** —— 粒子用 `mix-blend-mode: screen` 叠加，只发光、不压暗人物。
- **鼠标 / 触摸兜底** —— 没有摄像头也能玩。

---

## 🚀 部署到 GitHub Pages / Deploy

```bash
# 1. 在本目录初始化并推送
git init
git add .
git commit -m "init: air particle draw"
git branch -M main
git remote add origin https://github.com/jiantong183/air-particle-draw.git
git push -u origin main
```

```text
# 2. 打开仓库 Settings → Pages
#    Source 选 "Deploy from a branch"
#    Branch 选 main / (root)，保存
# 3. 等一两分钟，访问 https://jiantong183.github.io/air-particle-draw/
```

本地预览（需要 localhost 才能开摄像头）：

```bash
python3 -m http.server 8000
# 然后浏览器打开 http://localhost:8000/
```

---

## 🛠️ 技术栈 / Tech Stack

- 原生 HTML / CSS / JavaScript，**无构建步骤、无框架**。
- [MediaPipe Hands](https://developers.google.com/mediapipe)（通过 jsDelivr CDN 加载，浏览器本地推理，画面不上传）。
- Canvas 2D 粒子系统 + One Euro Filter + 二次贝塞尔平滑。

---

## 🎛️ 自定义 / Tweaks

打开 `index.html`，常用可调参数：

- 笔画粗细：`strokePath()` 里的 `pass(7, …)`（外发光宽度）与 `pass(2.6, …)`（白色亮芯宽度）。
- 抑抖强度：`makeEuro()` → `OneEuro(1.6, 0.03, 1.0)`。第一个值调小=更稳更跟手稍慢；调大=更跟手但稍抖。
- 捏合灵敏度：`onResults` 里的 `ratio<0.50`（落笔阈值）与 `ratio>0.62`（抬笔阈值）。
- 缩放上限：`const view={scale:1,min:1,max:4}` 的 `max`。
- 退出缩放缓冲：`drawGuard=8`（帧）。

---

## 🌐 浏览器支持 / Browser Support

Chrome / Edge / Safari 桌面端体验最佳。需要支持 `getUserMedia` 与 WebAssembly。
Best on desktop Chrome / Edge / Safari. Requires `getUserMedia` and WebAssembly.

---

## 📄 许可证 / License

MIT License，详见 [LICENSE](./LICENSE)。可自由使用、修改、分发。
MIT — free to use, modify, and distribute. See [LICENSE](./LICENSE).

## 🙏 致谢 / Acknowledgements

- 手部追踪 / Hand tracking: Google **MediaPipe Hands**
- 抑抖算法 / Smoothing: **1€ Filter** (Casiez, Roussel, Vogel)
