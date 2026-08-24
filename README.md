# 妙彩幻想曲 v13 · 部署与分享说明

## 已包含文件
- `index.html` — 完整游戏（单文件，所有 CSS/JS/SVG 内联，无外部依赖）
- `share.html` — 含 QR 码的扫码分享页
- `qr-lan.png` — 局域网 QR 码（指向 192.168.31.162:8770）

## 三种分享方式（按推荐度）

### 方式一 · 局域网内扫码体验（最简单）
1. 手机连接电脑所在的同一 WiFi
2. 手机微信扫描 `share.html` 里的二维码，或直接打开 `http://192.168.31.162:8770/share.html`
3. 即可在微信内置浏览器中游玩，**音效、动画全部完整运行**
4. 关电脑后游戏不可用（依赖本地服务器）

### 方式二 · 用 Cloudflare 隧道生成公网链接（推荐，可发给朋友）
1. 下载 cloudflared：访问 https://github.com/cloudflare/cloudflared/releases 下载 `cloudflared-windows-amd64.exe`
2. 双击 cloudflared.exe，让本地 8770 端口暴露为公网 HTTPS：
   ```
   cloudflared tunnel --url http://localhost:8770
   ```
3. 终端会输出形如 `https://xxxx.trycloudflare.com` 的链接
4. 把这个链接发到微信群里，所有人都能扫码打开游玩

### 方式三 · 上传到静态托管（最稳定，长期可用）
免费静态托管平台（任选其一）：
- **Vercel** (推荐)：拖拽 `dist/` 文件夹到 https://vercel.com/new 即可发布，得到 `.vercel.app` 永久链接
- **Netlify Drop**：访问 https://app.netlify.com/drop 拖入 `dist/` 文件夹，得到 `.netlify.app` 链接
- **GitHub Pages**：建仓库上传 `index.html`，在 Pages 设置启用即可

发布后将链接发到微信，别人扫码即可在微信中游玩。

## 如果想发到远方的朋友（4G/5G 网络下打开）
上述方式二/方式三 生成的公网 HTTPS 链接在微信中：
1. 长按链接 → 转发给朋友/群
2. 朋友点击链接 → 在微信内置浏览器打开
3. 完整可玩，含背景音乐 + 点击/消除/胜利/失败音效 + 顶堆不同图标

## 当前版本特性
- ✅ 20 关难度递增（图标种类 5→20，卡数 15→60）
- ✅ 顶堆每堆 3 张**互不相同**图标（避免原版"上下全同"无意义设计）
- ✅ Web Audio 合成 BGM（C 大调循环 + 低音铺底）
- ✅ 点击音效 / 消除音效 / 胜利音效 / 失败音效
- ✅ 右上角静音按钮可一键开关声音
- ✅ 移动端等比缩放 + 微信内置浏览器兼容
- ✅ 严格遮挡判定（被上层压住 >20% 不可选）

## 本地预览
```
node .shots/serve.cjs
```
然后浏览器访问 `http://localhost:8770/`
