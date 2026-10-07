# dexter-seeyue

[SeeYue](https://github.com/jinghu-moon/typora-see-yue-theme) 主题的魔改自用版，用在 Typora 上。

上游版本 v1.4.0，含 Dark / Pure / Salt 三套配色。上游 CSS 一共 53 个文件，本仓库只动了下面列出的几个，其余与上游一字不差，方便日后照着上游升级。

## 相比上游改了什么

### 一、修正类（上游的 bug / 平台差异）

| 问题 | 改法 | 文件 |
| --- | --- | --- |
| macOS 上侧边栏整块白底、配白字看不见 | 补上 Typora 核心真正读取的变量 `--bg-color` / `--side-bar-bg-color` / `--text-color` | `MySeeYue/CSS/configs/*-config.css` |
| 标题等级提示、引用块竖线、代码块语言标签、列表层级线全跑到正文左上角 | `#write` 的 `position: static` 改回 `relative`，恢复定位基准 | `MySeeYue/CSS/write-area.css` |

### 二、观感调整（写在自己的配置区里）

| 项目 | 改法 | 文件 |
| --- | --- | --- |
| 正文标题左侧的 H1~H6 小标签 | 关掉（打开侧边栏时会压住侧边栏图标） | `MySeeYue/CSS/configs/*-config.css` |
| 长表格、长代码块内部滚动 | 关掉（只有 Dark 关，`50vh` → `initial`） | `MySeeYue/CSS/configs/dark-config.css` |
| 图片最大宽度 | `85%` → `100%`（大图缩到正文宽，小图不放大） | `MySeeYue/CSS/configs/*-config.css` |
| 鼠标悬停图片放大 | 关掉（只有 Dark 关，`1.02` → `1`） | `MySeeYue/CSS/configs/dark-config.css` |

### 三、自定义样式（`MySeeYue/CSS/custom/custom-{dark,pure,salt}.css`）

主题作者预留的「升级不覆盖」区域，三套配色各写了一份，内容基本一致：

- **高亮改成圆角色块**：去掉自带的「马克笔涂抹」内阴影，改成 `#1f7a2e` 底 + 白字（对比度 5.41:1，够 WCAG AA）。
- **H2 并入 H3/H4 色系**：去掉 H2 的蓝色渐变底条和下方蓝线，正文层级只靠字号区分；标题里的链接改成「继承字色 + 下划线」，不再叠背景和网站小图标。
- **大纲小三角悬浮色去橙**：上游占暗色 / Salt 下悬停会变橙 `#e87040`，统一改成「三角保持本色 + 选中蓝半透明底衬」。
- **侧边栏顶部 H1~H6 图例**：白线不再压进目录区，图例挪到白线之上。
- Dark 那份里另有几段注释掉的备选样式（代码块当前行底色、单行横向滚动等），要哪个取消注释即可。

> 三份 custom 文件互不共用，改高亮这类公共效果时记得三份一起改。

### 四、文件重命名

- 文件夹：`SeeYue/` → `MySeeYue/`
- 入口：`see-yue-{dark,pure,salt}.css` → `my-see-yue-{dark,pure,salt}.css`
- 入口内容与上游相同，只是把 `@import` 路径改成了 `./MySeeYue/`。

## 目录结构

```
theme/
├── my-see-yue-dark.css     # 入口：暗色
├── my-see-yue-pure.css     # 入口：纯白
├── my-see-yue-salt.css     # 入口：盐系
└── MySeeYue/
    ├── CSS/                # 样式主体
    │   ├── configs/        # 三套配色集中在这里，改颜色、尺寸、开关都看这
    │   ├── custom/         # 自己的样式写这里，升级主题不会被覆盖
    │   └── ...
    ├── Fonts/              # 主题自带字体
    └── Images/             # 背景图、网站图标等
```

## 安装

把三个 `my-see-yue-*.css` 和 `MySeeYue/` 文件夹一起放进 Typora 的主题目录（两者必须同级，入口里是按 `./MySeeYue/` 找的）：

- macOS：`~/Library/Application Support/abnerworks.Typora/themes/`
- Windows：`%APPDATA%\Typora\themes\`
- Linux：`~/.config/Typora/themes/`

然后 Typora → 偏好设置 → 外观 → 主题，选 `my-see-yue-dark` / `my-see-yue-pure` / `my-see-yue-salt`。

## 想改哪里

- 配色、字号、各种开关：`MySeeYue/CSS/configs/{dark,pure,salt}-config.css`，文件内注释很全。
- 自己新加的效果：`MySeeYue/CSS/custom/custom-{dark,pure,salt}.css`。
- 换字体：把字体丢进 `MySeeYue/Fonts/`，改 `CSS/fonts.css`。

## 致谢

主题原作 [SeeYue](https://github.com/jinghu-moon/typora-see-yue-theme) © jinghu-moon，本仓库只是个人自用的改动版，字体与图片资源都来自上游、未作修改。使用前请遵守原作者的许可约定。
