# map.cq.je — MapLibre 网页地图

干净实用的单文件网页地图：OpenFreeMap 街道矢量 + Esri 卫星 / 混合图。

## 功能

- 街道图（[OpenFreeMap](https://openfreemap.org/) Liberty，无需 API Key）
- 高清卫星图（Esri World Imagery）
- 混合图（卫星 + OpenFreeMap 道路/注记）
- Nominatim 地点搜索
- 定位当前位置
- 点击显示经纬度
- 响应式（手机可用）

## 配置

编辑 `index.html`：

```js
const ESRI_API_KEY = "YOUR_ESRI_API_KEY";
```

未配置时回退到公开 ArcGIS World Imagery 瓦片。

## 本地运行

```bash
python3 -m http.server 8080
# 打开 http://localhost:8080
```

请用本地静态服务器打开（不要直接 `file://`），以便定位与跨域请求正常。

## 部署

将 `index.html` 放到任意静态托管即可：

- Nginx / Apache / GitHub Pages / Cloudflare Pages / Vercel / Netlify
- 建议启用 HTTPS（定位 API 需要安全上下文）
- 保留 MapLibre 自带 attribution（含 OpenFreeMap / OSM / Esri）

## 技术栈

- [MapLibre GL JS](https://maplibre.org/)（CDN）
- [OpenFreeMap](https://tiles.openfreemap.org/styles/liberty)
- Esri World Imagery
- OpenStreetMap Nominatim
