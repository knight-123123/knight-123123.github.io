# 个人技术博客

这是一个基于 Jekyll 的个人技术博客网站，专注于分享编程、算法和 Web 开发相关内容。

## 功能特点

- 响应式设计，完美适配桌面和移动设备
- 文章分类和标签系统
- 作者简介页面
- 现代化 UI 设计，包含优雅的动画效果
- 代码高亮显示
- 支持中英文内容

## 技术栈

- Jekyll 4.4.1 静态网站生成器
- Sass/SCSS 样式预处理
- 响应式 CSS 布局
- Font Awesome 图标库
- Google Fonts 网络字体

## 目录结构

```
.
├── _authors/         # 作者简介页面
├── _data/            # 网站配置数据
├── _includes/        # 可重用的 HTML 组件
├── _layouts/         # 页面布局模板
├── _posts/           # 博客文章 
├── _sass/            # SCSS 样式文件
│   ├── base/         # 基础样式和变量
│   ├── components/   # 组件样式
│   ├── layout/       # 布局样式
│   ├── pages/        # 页面特定样式
│   └── utils/        # 工具类和动画
├── assets/           # 静态资源
│   ├── css/          # 编译后的 CSS
│   └── images/       # 图片资源
├── _config.yml       # Jekyll 配置文件
├── .github/          # GitHub 配置文件
├── Gemfile           # Ruby gem 依赖
└── index.html        # 网站首页
```

## 安装和本地运行

### 先决条件

- Ruby 3.0 或更高版本
- RubyGems
- GCC 和 Make (使用 `sudo apt-get install gcc make` 安装在 Ubuntu)

### 安装步骤

1. 克隆仓库
   ```bash
   git clone https://github.com/knight-123123/knight-123123.github.io.git
   cd knight-123123.github.io
   ```

2. 安装 Jekyll 和 Bundler
   ```bash
   gem install jekyll bundler
   ```

3. 安装依赖
   ```bash
   bundle install
   ```

4. 本地运行
   ```bash
   bundle exec jekyll serve
   ```

5. 打开浏览器访问 `http://localhost:4000`

## 部署

### GitHub Pages

本博客配置为使用 GitHub Actions 自动部署到 GitHub Pages。每当推送到 `main` 分支时，会自动构建并部署网站。

1. 在仓库中设置 GitHub Pages:
   - 进入仓库设置 → Pages
   - 选择 "GitHub Actions" 作为源

2. 确保 `.github/workflows/jekyll.yml` 文件已正确配置

> 说明：使用 GitHub Actions 部署时，`_site/` 是构建产物（生成目录），不建议提交到 `main` 分支。
> 仓库已通过 `.gitignore` 忽略 `_site/`，由 CI 在部署时自动生成并发布到 `gh-pages`。

如果你的仓库历史上已经提交过 `_site/`，建议执行一次“取消跟踪”（不会删除你本地文件，只是让 Git 不再把它当源码）：

```bash
git rm -r --cached _site
git add .
git commit -m "Stop tracking _site build output"
git push
```

### 手动部署

如果您想手动部署到其他平台:

1. 构建网站
   ```bash
   bundle exec jekyll build
   ```

2. 构建好的网站将位于 `_site` 目录中，上传这些文件到您的托管服务

> 如果您选择“手动部署/自行托管”，可以使用 `_site/` 目录的内容进行发布；但在本仓库的默认方案（GitHub Actions）下，仍建议不要把 `_site/` 提交进源码分支。

## 自定义

### 添加新文章

1. 在 `_posts` 目录中创建新的 Markdown 文件，文件名格式为:
   ```
   YYYY-MM-DD-title.md
   ```

2. 在文件顶部添加 front matter:
   ```yaml
   ---
   layout: post
   title: "文章标题"
   author: your_author_id
   categories: [分类1, 分类2]
   tags: [标签1, 标签2]
   ---
   ```

3. 在 front matter 后添加文章内容

> 摘要控制：在文章正文中插入 `<!--more-->`，列表页（首页/博客/分类/标签等）将优先展示该标记之前的内容作为摘要。

### 添加新作者

1. 在 `_authors` 目录中创建新的 Markdown 文件，如 `your_author_id.md`
2. 添加作者信息:
   ```yaml
   ---
   short_name: your_author_id
   name: Your Full Name
   position: Your Position
   social:
     github: your_github_username
     email: your_email@example.com
   ---
   
   作者简介内容...
   ```

### 自定义样式

主要样式文件位于 `_sass` 目录中:

- `_sass/base/_variables.scss`: 修改颜色、字体等基础变量
- `_sass/components/`: 修改特定组件样式
- `_sass/layout/`: 修改整体布局样式

## 样式定制指南

### 修改颜色主题

编辑 `_sass/base/_variables.scss` 文件:

```scss
$primary-color: #your-color;    // 主色调
$secondary-color: #your-color;  // 辅助色
$accent-color: #your-color;     // 强调色
```

### 修改装饰线长度

网站使用多处装饰线元素，可以在以下文件中修改:

- `_sass/layout/_page.scss`: 页面标题下方的线条
- `_sass/pages/_home.scss`: 首页标题下方的线条
- `_sass/pages/_post.scss`: 文章内 H2 标题下方的线条
- `_sass/components/_cards.scss`: 卡片标题下方的线条
- `_sass/pages/_categories.scss`: 分类页面标题下方的线条 
- `_sass/layout/_footer.scss`: 页脚标题下方的线条

每个文件中可以修改 `width` 属性来调整线条长度:

```scss
&::after {
  width: 60px; // 修改这个值来调整线条长度
}
```

## 贡献指南

欢迎提交 Pull 请求以改进这个博客!

1. Fork 这个仓库
2. 创建您的特性分支 (`git checkout -b feature/amazing-feature`)
3. 提交您的更改 (`git commit -m 'Add some amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 开启一个 Pull 请求

## 联系方式

Zhou Zhouyou - 312847325@qq.com

项目链接: [https://github.com/knight-123123/knight-123123.github.io](https://github.com/knight-123123/knight-123123.github.io)