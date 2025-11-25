# Vue3 + TailwindCSS + Supabase 登录页面

这是一个使用Vue3、TailwindCSS和Supabase构建的科技简约风格登录页面。

## 特性

- 现代科技简约设计
- 响应式布局
- Supabase身份验证集成
- 加载状态指示器
- 表单验证
- 渐变背景和毛玻璃效果

## 技术栈

- Vue3 (Composition API)
- TailwindCSS (v4.0+)
- Supabase
- Vite (构建工具)

## 安装和运行

1. 安装依赖：
```bash
npm install
```

2. 复制环境变量文件：
```bash
cp .env.example .env
```

3. 编辑 `.env` 文件并填入你的Supabase项目配置：
```env
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here
```

4. 启动开发服务器：
```bash
npm run dev
```

5. 在浏览器中访问 `http://localhost:5173`

## 配置说明

### Supabase 设置

1. 访问 [Supabase](https://supabase.com) 并创建新项目
2. 在项目设置中找到你的 API URL 和匿名密钥
3. 将这些值添加到 `.env` 文件中

### 功能说明

- **登录功能**：使用 Supabase 的 `signInWithPassword` 方法
- **表单验证**：前端验证和后端错误处理
- **加载状态**：在登录过程中显示加载动画
- **错误处理**：显示来自 Supabase 的错误消息

## 文件结构

```
src/
├── components/
│   └── LoginPage.vue     # 登录页面组件
├── App.vue               # 主应用组件
├── main.js              # 应用入口
├── style.css            # TailwindCSS 样式
```

## 自定义

你可以轻松自定义以下内容：

- 颜色方案：修改 TailwindCSS 类
- 布局：调整组件中的 HTML 结构
- 功能：扩展 Supabase 认证逻辑

## 部署

要构建生产版本：

```bash
npm run build
```

构建后的文件将位于 `dist/` 目录中。

## 安全注意事项

- 确保 `.env` 文件不被提交到版本控制系统
- 在生产环境中使用适当的环境变量管理
- 遵循 Supabase 的安全最佳实践