# Parking Roster

一个使用 GitHub Pages 托管的静态员工停车位轮换网页。

## 文件
- `index.html`：网页入口与界面。
- `data.json`：员工、年假、暂停、办公室关闭和设置数据。
- `DATA_GUIDE.md`：字段解释与维护说明。

## GitHub Pages 部署
1. 在 GitHub 创建一个仓库，例如 `parking-roster`。
2. 上传以上三个文件到仓库根目录。
3. 打开仓库 Settings → Pages。
4. 在 Build and deployment 中选择 `Deploy from a branch`。
5. 选择 `main` 分支和 `/ (root)`，保存。
6. 等待 GitHub Pages 发布，然后使用显示的网址访问。

## 修改并发布数据
1. 在网页里进入员工管理、年假与暂停或办公室关闭页面进行修改。
2. 进入“数据管理”下载新的 `data.json`。
3. 打开 GitHub 仓库，上传并覆盖旧 `data.json`。
4. 等待网页更新。员工重新打开或刷新网页后会读取新数据。

## 重要限制
这是纯静态 GitHub 方案，没有登录和数据库。网页内修改不会自动写回 GitHub；管理员需要手动上传新 JSON。若仓库公开，数据也公开，请勿存储敏感信息。
