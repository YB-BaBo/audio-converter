# NCM 转 MP3（大陆静态托管包）

本目录是可直接上传到静态网站存储的站点文件。页面解密 NCM 文件、生成下载内容均在浏览器本机完成；FLAC 转 MP3 使用随包提供的 FFmpeg WebAssembly 组件，不依赖 jsDelivr 等境外 CDN。

## 上传与发布

1. 将本目录中的**全部内容**上传至腾讯云 COS 存储桶的网站根目录，目录结构保持不变；设置默认首页为 `index.html`。
2. 绑定你自己的已完成 ICP 备案的域名，并按 COS 控制台提示完成域名解析与 HTTPS 证书配置。请勿把旧的 `workers.dev` 地址当作大陆访问域名。
3. 用手机/电脑浏览器通过 HTTPS 域名打开页面，测试选择一个合法的 `.ncm` 文件；建议另测 FLAC 音轨转 MP3，以确认大体积 WASM 文件也能正常读取。

没有自有且已备案的域名时，本包仍可部署到 COS 做预览，但不能据此保证大陆网络下稳定正常访问；本包本身不会替你注册域名、备案或发布站点。

## 包含文件

- `index.html`：页面及 NCM 本地解密逻辑。
- `assets/ffmpeg/ffmpeg.js`、`814.ffmpeg.js`：FFmpeg 浏览器运行时。
- `assets/ffmpeg/ffmpeg-core.js`、`ffmpeg-core.wasm`：转码核心；WASM 文件约 31 MB。
- `THIRD-PARTY-NOTICES.md`：第三方组件版本与上游信息。

请保持 `assets/ffmpeg/` 相对路径及所有文件完整。站点需要 HTTPS（或 localhost）才能使用浏览器 Web Crypto API。FLAC 转码首次使用仍会从你自己的站点读取约 31 MB WASM；MP3 NCM 文件则直接解密，不需要加载该组件。
