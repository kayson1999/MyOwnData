# 📦 MyOwnData 数据管理指南

本仓库是个人主页的数据源，网站会通过 GitHub API 自动读取此仓库中的数据文件。

---

## 📁 目录结构

```
data/
├── home.json                  # 首页数据
├── projects.json              # 项目列表
├── tools.json                 # 工具列表
├── games.json                 # 游戏列表
├── blog/                      # 博客（思考与记录）
│   ├── index.json             # 文章索引（所有分类共用）
│   ├── xxx.md                 # 文章正文（Markdown 格式）
│   └── ...
├── knowledge/                 # 知识库
│   ├── index.json             # 知识库文档索引
│   ├── notes.json             # 笔记数据
│   ├── xxx.md                 # 知识库文章正文
│   └── ...
├── music/                     # 音乐
│   ├── xxx.mp3                # 音频文件
│   ├── xxx歌词.txt            # 歌词文件
│   └── ...
└── media/                     # 媒体资源
    └── files/                 # 通用媒体文件
```

---

## ✍️ 博客（思考与记录）

博客页面对应网站的「思考与记录」板块，支持以下分类：**全部**、**生活**、**音乐**、**电影**、**读书**。

### 添加普通文章（生活 / 电影 / 读书 等）

#### 第 1 步：编写 Markdown 文章

在 `data/blog/` 目录下创建 `.md` 文件，例如：`我的读书笔记2026-04-15.md`

#### 第 2 步：在 `data/blog/index.json` 中添加索引

```json
{
  "id": 3,
  "title": "我的读书笔记",
  "category": "读书",
  "categoryKey": "reading",
  "date": "2026-04-15",
  "excerpt": "最近读了一本好书，分享一些感悟...",
  "tags": ["读书", "笔记"],
  "readTime": 5,
  "file": "我的读书笔记2026-04-15.md",
  "enabled": true,
  "pinned": false,
  "order": 10
}
```

#### 字段说明

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `id` | number | ✅ | 唯一标识，递增即可 |
| `title` | string | ✅ | 文章标题 |
| `category` | string | ✅ | 分类名称（中文），可选值：`生活`、`音乐`、`电影`、`读书`、`随笔` |
| `categoryKey` | string | ✅ | 分类标识（英文），对应：`life`、`music`、`movie`、`reading`、`life` |
| `date` | string | ✅ | 发布日期，格式 `YYYY-MM-DD` |
| `excerpt` | string | ✅ | 文章摘要，显示在列表卡片上 |
| `tags` | string[] | ✅ | 标签数组 |
| `readTime` | number | ✅ | 预计阅读时间（分钟） |
| `file` | string | ✅ | 对应的 Markdown 文件名（放在 `data/blog/` 下） |
| `enabled` | boolean | ❌ | 是否上架，默认 `true`，设为 `false` 可隐藏 |
| `pinned` | boolean | ❌ | 是否置顶，默认 `false` |
| `order` | number | ❌ | 排序权重，数字越小越靠前，默认 `999` |

### 添加音乐类文章

音乐类文章比较特殊，不需要 `.md` 文件，而是关联音频和歌词文件：

```json
{
  "id": 4,
  "type": "music",
  "title": "我的新歌",
  "category": "音乐",
  "categoryKey": "music",
  "date": "2026-04-15",
  "excerpt": "一首新歌的创作分享",
  "tags": ["原创", "说唱"],
  "readTime": 3,
  "audioFile": "我的新歌-20260415.mp3",
  "lyricsFile": "我的新歌歌词.txt",
  "coverColor": "linear-gradient(135deg, #FF4500 0%, #FF6B9D 50%, #B14EFF 100%)",
  "enabled": true,
  "pinned": false,
  "order": 5
}
```

#### 音乐类额外字段

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `type` | string | ✅ | 固定为 `"music"` |
| `audioFile` | string | ✅ | 音频文件名，放在 `data/music/` 目录下 |
| `lyricsFile` | string | ❌ | 歌词文件名，放在 `data/music/` 目录下 |
| `coverColor` | string | ❌ | 封面渐变色，CSS gradient 格式 |

> ⚠️ 音频文件放在 `data/music/` 目录下，不是 `data/blog/` 目录。

---

## �� 知识库

### 添加知识库文档

#### 第 1 步：编写 Markdown 文档

在 `data/knowledge/` 目录下创建 `.md` 文件。

#### 第 2 步：在 `data/knowledge/index.json` 中添加索引

```json
{
  "id": 2,
  "title": "Java 并发编程指南",
  "desc": "深入理解 Java 多线程与并发工具",
  "tags": ["Java", "并发"],
  "file": "java-concurrency.md",
  "enabled": true,
  "pinned": false,
  "order": 10
}
```

### 添加笔记

在 `data/knowledge/notes.json` 中直接添加笔记数据。

---

## 🚀 项目

在 `data/projects.json` 中添加项目条目：

```json
{
  "id": 3,
  "title": "我的新项目",
  "desc": "项目描述...",
  "tags": ["Vue", "Node.js"],
  "cover": "",
  "features": ["功能1", "功能2"],
  "github": "https://github.com/xxx/xxx",
  "demo": "https://xxx.com",
  "enabled": true,
  "pinned": false,
  "order": 10
}
```

---

## 🛠️ 工具 & 🎮 游戏

分别在 `data/tools.json` 和 `data/games.json` 中添加条目。

---

## 📝 通用管理字段说明

所有数据条目都支持以下管理字段：

| 字段 | 默认值 | 说明 |
|------|--------|------|
| `enabled` | `true` | 设为 `false` 可隐藏该条目（不删除数据） |
| `pinned` | `false` | 设为 `true` 会置顶显示 |
| `order` | `999` | 排序权重，数字越小越靠前 |

排序优先级：**pinned 置顶 > order 数值升序**

---

## 🔄 数据更新流程

1. 在本仓库中修改/添加数据文件
2. `git add . && git commit -m "添加新文章" && git push`
3. 网站会自动通过 GitHub API 读取最新数据，无需重新部署
