CS-091 手机可访问商品测试网站

本包包含 index.html 和 product.json。是完整的静态网站源码，但下载后并不会自动出现在公网。

最快发布方式（无需服务器）：
1. 打开 https://app.netlify.com/drop （需按平台要求登录）。
2. 将包含 index.html 和 product.json 的整个目录拖放上传。
3. 等待生成 https://xxxx.netlify.app/ 网址。
4. 在手机浏览器打开该网址，确认能看到价格 ¥599、缺货。
5. 将该公开网址交给你的 Agent 设定价格/补货定时监控。

修改价格/库存以制造触发事件：
- 在目录中的 product.json 把 price 改为 499，stock 保持 0；或用 product_price_499.json 内容替换 product.json。
- 补货测试把 price 保持 599、stock 改为 12；或用 product_restock.json 内容替换 product.json。
- 重新上传整个站点目录到原有 Netlify 站点的 Deploys 页面，确保新部署使用同一个域名；不要简单通过 Drop 创建一个新的随机域名。
- 公网页面刷新后即可看到新数据；如果部署/CDN 有延迟，等更新可见再检查。

更适合频繁改价：GitHub Pages
1. 新建公开仓库，并在仓库根目录提交 index.html、product.json。
2. Settings -> Pages -> Deploy from branch -> main / (root)。
3. 等待 Pages 发布，使用 https://用户名.github.io/仓库名/ 访问。
4. 需要修改时，直接在 GitHub 网页编辑 product.json 并提交；等待网站重新部署。
5. 注意：Github Pages 不保证精确的秒级实时更新。首次监控应读取初始状态，后续对比状态变化。

推荐 Agent 指令：
请每天检查该商品测试网页及其 product.json。首次检查记录价格、库存且不发送通知。价格由>=500变为<500时或库存由0变为>0时提醒；相同状态不要重复提醒。无变化不提醒。提醒须包含商品、价格、库存和检查时间。不要购买或下单。若获取失败，报告错误，不可编造价格。

提醒：本包提供静态站点文件；真实的定时提醒和推送，需要由被测试 Agent 的定时任务系统完成。
