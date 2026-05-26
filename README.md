# MyLandlordApp — 简易房东管理 PWA（单文件实现）

概述
- 单文件 PWA：`index.html`（原生 HTML/CSS/JS），使用 `localStorage` 持久化。
- 目标：逐步迭代实现房屋与租客管理、搜索与支付状态追踪。

已实现（步骤 1–6）
1. 登录（本地验证）：用户名 `admin` / 密码 `123456`，登录状态保存在 `localStorage`（键 `landlord_auth`）。
2. 房屋管理：添加/删除房屋，房屋存储键为 `landlord_data`。
3. 智能搜索：实时搜索地址/编号，按匹配度评分排序。
4. 房屋详情页：进入房屋查看详情并管理租客。
5. 租客 CRUD：添加/编辑/删除租客，字段包括 `name, phone, monthlyRent, deposit, moveInDate, rentDay, paid`。
6. 支付状态（红绿灯）：租客卡片可切换支付状态，主界面显示汇总（已收/未收金额）。
7. 收尾：用 `createElement`/`textContent` 替代 `innerHTML`（减少 XSS 风险），添加多标签同步（`storage` 事件）。

如何本地运行
- 直接在浏览器打开（注意：部分浏览器对 `file://` 有限制）：
  `file:///Users/<your>/Desktop/MyLandlordApp/index.html`
- 推荐启动本地静态服务器：
```bash
cd ~/Desktop/MyLandlordApp
python3 -m http.server 8000
# 然后访问 http://localhost:8000/index.html
```

线上同步（Firebase）
- 当前 `index.html` 已加入可选 Firebase 云端同步支持。
- 你只需创建 Firebase 项目并将配置填入 `index.html` 中的 `firebaseConfig`。
- 开启 Firestore 数据库（测试模式）后，多个设备即可共享同一份房屋与租客数据。
- 如果没有配置，应用仍会继续使用本地 `localStorage`。

验收清单（简短）
- 登录：`admin` / `123456`。
- 添加一个或多个房屋，检查列表显示。
- 搜索：根据地址或编号检索并按相关性排序。
- 进入某房屋，添加租客，切换支付状态（红/绿），返回主界面验证汇总金额。
- 在浏览器 DevTools → Application → Local Storage 查看 `landlord_data`、`landlord_sys_credentials` 与 `landlord_auth`。

下一步建议（可选）
- 注册 Service Worker 以支持离线缓存与真正的 PWA 安装体验。
- 提供简单图标与 `manifest.json` 文件（当前使用内联 data manifest 占位）。
- 添加导出/导入（JSON）功能，便于备份/迁移数据。
- 更严格的表单校验、输入消毒与国际化支持。
- 将单文件拆分为静态资源（`index.html`, `app.js`, `styles.css`）便于维护和单元测试。

我可以现在：
- (A) 帮你创建并注册一个简单的 Service Worker；
- (B) 拆分当前单文件为 `app.js`/`styles.css`；
- (C) 生成 `README` 中建议的快速实现清单并继续第八步。 

请选择要我继续的项，或说明你希望我做的其它收尾工作。