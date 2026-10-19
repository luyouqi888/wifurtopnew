# 路绒Lab 旧域名引导页 v1.0.0 · 2026-10-19

基于 v2.8.18 的原始蓝白渐变首屏精简。只有路绒Lab、欢迎英文和黑色“前往新网站”按钮，固定前往 https://wifurlab.com/ 。没有 Dock、导航、商城、登录、后台、API 代理或统计脚本，无需后端和环境变量。

## 预览

直接双击 dist/index.html 即可预览，不需要安装依赖或编译。

## Cloudflare Workers 部署

解压本包，在解压后的文件夹打开终端（Node.js 22 或更新版本）：

```sh
npm run build
npx wrangler@4 login
npm run deploy
```

Wrangler 配置已保留。项目名为 wifur-top-landing，防止覆盖新主站的 Worker。首次运行 npx 会下载 Wrangler；不需要 npm install。

先检查部署后输出的 workers.dev 地址。确认只有一个黑色按钮、电脑和手机显示正常，按钮前往新站。

随后在该 Worker 的“设置 → 域和路由”中添加 wifur.top 和 www.wifur.top 两个自定义域。若有冲突，先导出原 DNS 备份，再移除这两个名称指向旧 EdgeOne 的 CNAME，按 Cloudflare 提示完成绑定；不要改 api.wifurlab.com、新主站的解析或任何邮件 MX/TXT 记录，也不要恢复 api.wifur.top。

若通过 Workers 的 Git 构建部署：构建命令 npm run build，部署命令 npx wrangler@4 deploy，项目根目录使用本包根目录。

## 静态文件上传

如果使用 Cloudflare Pages 的静态上传，只上传 dist 文件夹内的文件即可。Wrangler 的上述命令部署到 Workers，与 Pages 上传是两种任选其一的方式。

这是独立引导页，不更改 Ubuntu、Nginx、新站后端或已经退役的旧 API。本包尚未代你部署到线上。

参考：https://developers.cloudflare.com/workers/static-assets/
