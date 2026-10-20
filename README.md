# map.cq.je — 高性能 CesiumJS 3D 地球地图

单文件网页版 3D 地球：卫星底图、图层切换、地点搜索、定位与点击坐标。

## 功能

- 默认 3D 地球（旋转 / 缩放 / 倾斜）
- 卫星图（Esri World Imagery）+ 街道图 / 地形图切换
- 地点搜索（OpenStreetMap Nominatim）
- 定位当前位置
- 点击显示经纬度
- 响应式 UI（手机 / 平板 / 电脑）

## 性能要点

代码中已标注关键参数，主要包括：

| 参数 | 作用 |
|------|------|
| `maximumScreenSpaceError` | 控制瓦片精度；移动端更高以减负 |
| `tileCacheSize` | 瓦片内存缓存上限 |
| `preloadWhenHidden` | 隐藏图层不预加载 |
| `RequestScheduler.maximumRequestsPerServer` | 限制并发瓦片请求 |
| `requestRenderMode` | 静止时不重绘，省电 |
| 按需地形 / 大气 / 光照 | 默认精简效果，按钮按需开启 |
| `#cesiumContainer` 背景色 | 首屏避免大面积空白 |

架构参考：Cesium Imagery Layers / Performance 示例、MapLibre 按需图层策略、谷歌地球式倾斜与飞行动画。

## 配置

编辑 `index.html` 顶部常量：

```js
const ESRI_API_KEY = "YOUR_ESRI_API_KEY";           // Esri API Key
Cesium.Ion.defaultAccessToken = "YOUR_CESIUM_ION_TOKEN"; // 开启「地形」时需要
```

未配置 Esri Key 时会回退到公开 ArcGIS World Imagery MapServer；地形功能需要有效的 [Cesium Ion](https://ion.cesium.com/) Token。

## 本地运行

因浏览器对地理定位 / 部分瓦片 CORS 的限制，请用本地静态服务器打开（不要直接双击 `file://`）：

```bash
# Python 3
python3 -m http.server 8080

# 或 Node
npx --yes serve -l 8080
```

浏览器访问：<http://localhost:8080>

## 部署

任意静态托管即可，例如：

- **Nginx / Apache**：将 `index.html` 放到站点根目录
- **GitHub Pages / Cloudflare Pages / Vercel / Netlify**：直接部署仓库，入口为 `index.html`
- 建议启用 HTTPS（定位 API 在多数浏览器中要求安全上下文）
- 生产环境请替换 `YOUR_ESRI_API_KEY` / `YOUR_CESIUM_ION_TOKEN`，并遵守各底图服务的使用条款（OSM Nominatim 请控制请求频率）

## 技术栈

- [CesiumJS](https://cesium.com/platform/cesiumjs/)（CDN）
- Esri World Imagery / World Topo Map
- OpenStreetMap 瓦片与 Nominatim 地理编码
