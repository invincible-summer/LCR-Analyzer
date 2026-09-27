# docs/show — 作品展示幻灯（硬件部分与软件功能介绍）

当前展示版为 14 页、16:9 的 HTML 幻灯，结构为：总标题 → 作品综述 → 硬件部分 → 软件部分（功能简介 + 电路辨识拟合展示）。

- **总标题（第 1 页）**：多功能LCR测量仪（张行言&杨钧富队，2026/9/19）。
- **作品综述（第 2–4 页）**：作品简介、功能介绍（整机接口标注与操作界面）。
- **硬件部分（第 5–11 页）**：子标题页、硬件总体方案框图（正弦信号生成方案借鉴 bitluni/ESP32-S3-VGA，框图页保留引用角标）、实测数据（R / C / L / 电容容量随频率变化 / 波特图）、正弦输出波形（12 / 123 / 1234 Hz 示波器实拍）。文字与图片内容原样迁自 `html-to-ppt/硬件部分_副本.pptx`；其中的实测数据图表原为 EMF 矢量图，已从其内嵌的矢量 PDF 以 4× 分辨率重渲染为 PNG（`assets/hw/`）。
- **软件部分（第 12–14 页）**：只介绍功能、不涉及实现——第 12 页为网页上位机功能总览（时域分析、扫频 Bode、电路辨识拟合、实时监测、实验历史、使用文档）；第 13–14 页为电路辨识拟合功能的实际运行截图（`assets/figs/`），展示自动识别出的等效电路、元件参数值，以及多候选结果的排序与对比。

## 在线展示

GitHub Pages：<https://invincible-summer.github.io/LCR-Analyzer-WebSite/>

页面由 `.github/workflows/pages-show.yml` 自动部署：只要 `main` 上 `docs/show/html-to-ppt/**` 更新，就会重新发布。部署时将 `slides.html` 复制为站点根目录的 `index.html`，其余 `assets/` 原样保留。

## 目录

| 版本 | 成品 | 源文件 | 重建方式 |
|---|---|---|---|
| HTML→PDF（精美版） | `html-to-ppt/LCR-硬件与软件功能.pdf` | `html-to-ppt/slides.html`（纯静态 HTML/CSS，无外部依赖；硬件图片在 `assets/hw/`，软件截图在 `assets/figs/`） | Chrome/Edge headless `--print-to-pdf`（页面尺寸 1280×720 px = 16:9） |
| PPTX | `html-to-ppt/LCR-硬件与软件功能.pptx` | 由上述 PDF 派生 | `pdftoppm -png -r 192` 渲染每页（2560×1440），python-pptx 将每页 PNG 整页插入 13.333 in × 7.5 in 幻灯 |

```sh
# HTML 版重建（任一 Chromium 系浏览器）
chrome --headless=new --no-pdf-header-footer --virtual-time-budget=25000 \
       --print-to-pdf=out.pdf file:///…/html-to-ppt/slides.html
```

## 讲解顺序

1. 总标题：多功能LCR测量仪
2. 作品简介
3. 功能介绍：整机外观与接口标注
4. 功能介绍：操作流程、五大功能与界面截图
5. 硬件部分子标题页
6. 硬件总体方案框图
7. 实测数据-R
8. 实测数据-C/L
9. 实测数据-电容容量随频率变化（趋势图与说明单页展示）
10. 正弦输出（12 / 123 / 1234 Hz 输出波形）
11. 实测数据-波特图测量
12. 软件部分功能简介：网页上位机功能总览
13. 电路辨识拟合：自动识别等效电路（实际运行截图）
14. 电路辨识拟合：多候选结果对比（实际运行截图）
