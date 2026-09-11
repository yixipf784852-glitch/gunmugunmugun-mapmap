# gunmugunmugun-mapmap

BanG Dream 同人角色面板用的静态资源托管。底图 + 地标数据，走 jsDelivr CDN 直链。

## 怎么用

URL 就是路径，没有映射表：

```
https://testingcf.jsdelivr.net/gh/yixipf784852-glitch/gunmugunmugun-mapmap@main/maps/01_ikebukuro.webp
https://testingcf.jsdelivr.net/gh/yixipf784852-glitch/gunmugunmugun-mapmap@main/data/landmark_kanto.json.gz
```

换掉 `maps/01_ikebukuro.webp` 就是换一张图。域名可选：

| 域名 | 说明 |
|---|---|
| `testingcf.jsdelivr.net` | 国内节点，默认用这个 |
| `cdn.jsdelivr.net` | jsDelivr 官方主域 |
| `raw.githubusercontent.com/yixipf784852-glitch/gunmugunmugun-mapmap/main/...` | 不走 CDN，注意没有 `@main` 而是 `/main/` |

> jsDelivr 单文件上限 20 MB。本仓库最大单文件 1.52 MB，安全。

## 目录

```
maps/    51 张 WebP 底图，41 MB，单张 ≤1.52 MB
         01–43  关东（东京都心 / 涩谷 / 池袋 / 镰仓 / 横滨 / 成田 …）
         45–52  东京中景东西半 + 大阪三张 + 京都三张
         （没有 44：那张 tokyo_mid_wide 只有 PNG/SVG 源，体积超标，未收）
data/    地标与 POI，各有 .json 和 .json.gz 两份
         landmark_{kanto,narita,chita,osaka,kyoto}.json(.gz)   共 1970 个地标
         poi_2020.json(.gz)                                    13068 个 POI
```

`.gz` 和未压缩 `.json` 都传了：前端按 gzip 魔数自动判断，哪份都能直接吃。CDN 万一对 `.gz` 处理异常，把链接改成同名 `.json` 即可。

## 回填链接

改了文件不用手工改前端，跑一次：

```bash
python tools/回填CDN链接.py --user yixipf784852-glitch --write
```

它读 `角色面板.html` 里每个 `{file:'xxx', url:'...'}`，按文件名算出 CDN 链接填回去。

## 许可

底图与地标数据均由 2020-12-31 的 OpenStreetMap 快照衍生。

**© OpenStreetMap contributors，ODbL 1.0**
https://www.openstreetmap.org/copyright

前端右上角的署名覆盖本仓库全部内容，别删。
