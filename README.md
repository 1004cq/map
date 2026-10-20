# map.cq.je — CesiumJS 3D 地球地图

单文件网页版 3D 地图：Esri 卫星 / OSM 街道 / 混合图，谷歌地图式扁平 UI。

## 功能

- 3D 地球（旋转 / 缩放 / 倾斜）
- 卫星图（Esri World Imagery）
- 街道图（OpenStreetMap）
- 混合图（卫星 + 注记）
- Nominatim 地点搜索
- 定位当前位置
- 点击显示经纬度
- 按需开启地形（需 Cesium Ion Token）
- 响应式（手机可用）

## 配置

编辑 `index.html`：

```js
const ESRI_API_KEY = "YOUR_ESRI_API_KEY";
const CESIUM_ION_TOKEN = "YOUR_CESIUM_ION_TOKEN"; // 仅「地形」需要
```

## 本地运行

```bash
python3 -m http.server 8080
# 打开 http://localhost:8080
```

请用本地静态服务器打开（不要直接 `file://`）。

## 部署

将 `index.html` 放到任意静态托管（Nginx / GitHub Pages / Cloudflare Pages / Vercel / Netlify）。建议启用 HTTPS。

## 性能要点

- `requestRenderMode`：静止不重绘
- `maximumScreenSpaceError` / `tileCacheSize` / `preloadWhenHidden`
- `RequestScheduler.maximumRequestsPerServer`（移动端更严）
- 移动端限制 `maximumLevel`
- 默认关闭地形；容器深色背景减少首屏空白

## 技术栈

- [CesiumJS](https://cesium.com/platform/cesiumjs/)（CDN）
- Esri World Imagery / Reference Labels
- OpenStreetMap 瓦片
- Nominatim
