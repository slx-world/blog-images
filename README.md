# blog-images

[完美世界](https://slx-world.top/)个人博客的图片资源仓库，用于保存文章截图、背景图、封面、SOP 流程图和主题图片。

本仓库负责存放图片，文章与主题代码位于 [hexo-shoka-source](https://github.com/slx-world/hexo-shoka-source)。博客图片统一通过图床引用，不再提交到博客源码仓库。

## 上传与访问方式

```text
写作上传：Typora → PicGo → GitHub / slx-world/blog-images（master 分支）
页面访问：浏览器 → images.weserv.nl → jsDelivr → GitHub 图片文件
```

GitHub 保存原始文件，jsDelivr 提供资源分发，weserv 提供图片代理、缓存和可选的尺寸处理。后两者的缓存并不替代原图备份，也不能保证所有网络环境下都能即时访问。

## PicGo 配置

在 PicGo 的 GitHub 图床设置中填写：

| 配置项 | 本仓库的填写方式 |
| --- | --- |
| 仓库名 | `slx-world/blog-images`，不要附加 `.git` |
| 分支 | `master`，不要误填为 `main` |
| Token | 本机保存的 GitHub 上传令牌，不写入本文或仓库 |
| 存储路径 | 可留空；新图片建议按内容设置，如 `test/python/` |
| 自定义域名 | 下方的链接前缀，不包含存储路径或文件名 |

自定义域名前缀：

```text
https://images.weserv.nl/?url=https://cdn.jsdelivr.net/gh/slx-world/blog-images@master
```

保存配置并设为默认图床，先上传一张测试图片，确认仓库中出现文件，且生成的地址能独立打开。不同版本的界面可能有所变化，以 [PicGo 官方配置说明](https://docs.picgo.app/zh/gui/guide/config)为准。

### Typora 写作流程

1. 在 Typora 的图像偏好设置中，将插入本地图片的处理方式设为上传图片。
2. 上传服务选择与本机安装方式一致的 PicGo；使用 PicGo 应用版时，配置对应程序路径。
3. 执行“验证图片上传选项”，确认上传链路可用。
4. 粘贴或插入图片后，检查 Markdown 中已经是远程图床 URL，而不是 `C:\…`、`D:\…` 或本地相对路径。
5. 发布文章前，再检查正文图片和封面是否能正常打开。

修改 PicGo 配置通常只影响后续上传，不能据此认为旧文章的图片链接也已自动更新。

## 图片链接格式

博客正文使用以下 Markdown 格式，地址中的路径必须与本仓库文件路径一致：

```markdown
![图片说明](https://images.weserv.nl/?url=https://cdn.jsdelivr.net/gh/slx-world/blog-images@master/20.jpg)
```

分类封面的实际链接示例：

```text
https://images.weserv.nl/?url=https://cdn.jsdelivr.net/gh/slx-world/blog-images@master/blog-assets/_posts/ai-app/cover.jpg
```

排查问题时，可以去掉外层代理，对照 jsDelivr 地址：

```text
https://cdn.jsdelivr.net/gh/slx-world/blog-images@master/20.jpg
```

需要缩略图时，可在外层地址后追加尺寸参数，如 `&w=1200`；正文展示图与高清原图链接应分开维护，避免长流程图的文字因缩小而无法辨认。原始文件仍保存在 GitHub，代理响应可能经过重新编码，不能用代理下载结果代替原文件做字节校验。参数与 URL 编码规则见 [weserv 官方文档](https://wsrv.nl/docs/)。

## 目录说明

以下为主要目录，省略具体文件：

```text
blog-images/
├── backend/                         # 数据库、框架等教程截图
├── bigdata/                         # 大数据教程截图
├── devops/                          # Git、Docker、Kubernetes 等截图
├── test/                            # 测试相关截图
├── blog-assets/                     # 从博客源码迁入的资源
│   ├── _posts/                      # 各分类封面
│   ├── ai-app/hermes-agent-course/  # Hermes 教程图片
│   ├── images/sop-flowcharts/       # SOP 流程长图
│   ├── friends/                    # 友链图片
│   ├── links/                      # 导航站点标志
│   └── theme-shoka/                 # 主题图片及上游示例资源
│       └── source/images/          # 头像、赞赏码、图标等
└── 根目录历史文件                   # 数字命名图片、人物图片、早期截图等
```

根目录还保留少量历史视频资源，不应通过 weserv 图片处理地址访问视频。

### 新文件命名约定

- 路径使用正斜杠 `/`，例如 `test/python/`，不要使用 Windows 反斜杠 `\`。
- 新文件优先使用英文、数字、短横线和时间戳，例如 `test/python/image-20260905111701611.png`；此处是命名示例，不表示该规范路径已存在。
- 保持扩展名、文件名大小写与实际文件一致；含中文和空格的既有路径应正确编码，不要擅自重命名。
- 优先新增带时间戳或版本后缀的文件，避免同名覆盖后出现缓存中的旧图。
- 不要仅因文件名或图片内容相似就删除“重复文件”，不同文章可能仍引用不同路径。

### 历史反斜杠路径

仓库中仍保留个别文件名，例如：

```text
\test\python\image-20260905111701611.png
```

对应旧链接中的 `%5C` 是反斜杠编码，并不等于目录分隔符 `/`。这些链接仍可能有效；不能只把 `%5C` 替换为 `/`，否则会指向不存在的文件。

如需规范历史路径，应先复制文件到新路径，验证新地址，再替换所有引用；确认没有遗留引用后才考虑删除旧文件。

## 与博客源码的配合

图片文件放在本仓库，以下配置仍在 [hexo-shoka-source](https://github.com/slx-world/hexo-shoka-source) 中维护：

| 使用位置 | 配置入口 |
| --- | --- |
| 文章正文与文章封面 | Markdown 图片链接与 Front Matter 的 `cover` |
| 分类卡片封面 | 根目录 `_config.yml` 的 `category_covers`，以分类 slug 为键 |
| 随机背景图 | `themes/shoka/_images.yml` |
| 主题图片地址前缀 | `themes/shoka/_config.yml` 的 `image_base` |

2026-09-05 的图片迁移保留了原始文件内容，未重写旧 Git 历史。原路径、新路径及原文件 Git Blob SHA 可查阅源码仓库的 [图片迁移清单](https://github.com/slx-world/hexo-shoka-source/blob/master/image-migration-manifest.json)。

在**博客源码仓库**中发布前运行：

```sh
npm run build
npm run test:images
```

这两条命令不在本图床仓库中运行。图片检查用于发现源码内的图片文件和生成页面中不符合约定的链接，不等同于逐一在线下载验证所有图片。

## 安全与维护

- 推荐使用只授权本仓库的细粒度 Token，图片上传所需的 `Contents` 设置为读写，其余权限不额外开放，并设置合理有效期。相关权限要求见 [GitHub 文件上传接口说明](https://docs.github.com/en/rest/repos/contents#create-or-update-file-contents)。
- 不上传 Token、PicGo 配置文件、密码、客户资料、未脱敏的内部截图或其他不应公开的信息；本仓库是公开资源。
- 图片发布前检查清晰度与体积。封面可以使用压缩后的展示版本，代码截图、报表和 SOP 长图优先保证文字可读，同时保留原图。
- 定期备份原图和仓库。Git 历史有助于恢复误删文件，但并非独立备份；删除当前文件也不会自动清除其历史版本。
- 敏感文件一旦公开，应按泄露处理；删除 GitHub 文件不保证第三方缓存立即消失，泄露的凭据应立即撤销。

## 常见问题

| 现象 | 建议检查 |
| --- | --- |
| PicGo 上传失败 | 仓库名、`master` 分支、网络、Token 有效期及仓库写入权限 |
| 上传成功但文章不显示 | Markdown 是否使用了新 URL，路径、大小写及编码是否一致 |
| jsDelivr 能打开，weserv 不能打开 | 对比代理响应、文件格式及处理参数，判断是否为代理链路故障 |
| 替换图片后仍显示旧图 | 多层缓存可能尚未刷新；优先上传新文件名并更新引用 |
| 图片偶尔显示、偶尔空白 | 区分网络请求失败、缓存和博客懒加载触发问题，不要仅凭刷新恢复就判断原因 |
| 准备清理旧图片 | 先搜索博客正文、封面配置、背景列表和主题中的引用，再删除 |

## 版权说明

本仓库用于个人博客资源管理，公开访问不代表仓库内所有图片均可自由转载或商用。第三方图片、人物素材和标志的权利归相应权利人所有；使用前请核实授权，仓库中的说明不替代原作品的授权条件。
