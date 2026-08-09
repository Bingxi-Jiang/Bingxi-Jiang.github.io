# GitHub Pages 图片与 Logo 修改指南

这个 ZIP 已经是可直接上传到 GitHub Pages 的静态版本。最安全的修改方式是：**保留原文件名和扩展名，直接用新图片覆盖旧图片**。这样不需要重新编译。

## 1. 主页 Featured Projects 与 Full Archive 已完全分开

主页与 Archive 现在使用两套独立封面。初始图片内容相同，但替换一边不会影响另一边。

| 页面 | 文件夹 | 推荐比例 |
|---|---|---|
| Home → Selected work | `media/projects/home/` | 2:1（横向） |
| Work → Project archive | `media/projects/archive/` | 2:1（横向） |

主页 Featured Projects 的四张封面：

1. `media/projects/home/noted.jpg`
2. `media/projects/home/flowcrusade.jpg`（FocusTrail）
3. `media/projects/home/syllabus-to-schedule.jpg`（Course Helper）
4. `media/projects/home/longevity-llm-benchmark.jpg`

Full Archive 的对应图片在 `media/projects/archive/`。例如，只想修改 Archive 的 Noted，就替换 `media/projects/archive/noted.jpg`；主页不会变化。

建议输出尺寸：2000×1000、1600×800 或其他 2:1 横图。界面会完整显示图片，不需要把 16:9 图片强行裁成竖图。

## 2. Experience 公司 Logo

公司 Logo 位于：

`media/logos/`

新版使用全彩的自适应品牌签名，不再灰度化，也不降低透明度，更不会强制放进 1:1 方框。网页会根据每个品牌的真实比例分别处理竖标、紧凑图标、横向 wordmark 与圆形校徽。Home 与 Work 页面共用同一套显示规则。

直接覆盖同名文件即可更新：

- `dassault-systemes.png`
- `gtechfin.png`
- `fresh-road.png`
- `ping-an.png`
- `uci.png`
- `uci-relational-cognition-lab.png`
- `uci-xie-lab.png`
- `deepem-lab.png`
- `cmu.png`

不需要转换为 SVG。PNG 可以保留原本的长宽比与品牌色，建议尽量使用透明背景。分辨率不必完全一致，只要可见图形本身清楚即可。

显示尺寸在根目录的 `v6-overrides.css` 中调整。搜索：

`Each signature gets a canvas suited to its actual artwork ratio`

例如 Fresh Road 当前使用：

```css
.company-logo:has(img[src*="fresh-road"]) {
  --logo-width: 216px;
  --logo-height: 52px;
}
```

改 `--logo-width` 与 `--logo-height` 就能单独改变这个品牌的显示空间，不会影响其他 Logo。

特殊情况：

- `ping-an.png` 原图是 2047×2047，但有效 Logo 位于中下部。CSS 已经补偿透明留白，不需要手工裁图。
- `deepem-lab.png` 与 `uci-relational-cognition-lab.png` 的棋盘格已经烘焙进图片，CSS 会把它们裁成圆章，隐藏四角棋盘格。
- 如果以后把 Ping An 换成已经紧密裁好的新图，请同时删除 `v6-overrides.css` 中 `Ping An ships on a square canvas` 下的特殊变换规则。

## 3. Homepage Field Notes 与详情页图片已分开

主页 Events attended 使用：

`media/field-notes/home/`

Field Notes 索引页和每篇详情页使用：

`media/field-notes/`

因此可分别裁图。例如，修改主页 TikTok 卡片只替换：

`media/field-notes/home/tiktok-private-session.jpg`

修改 TikTok 的 Field Notes 页面则替换：

`media/field-notes/tiktok-private-session.jpg`

其他文件名：

- `la-hacks.jpg`
- `pycon.jpg`
- `caltech-longevity.jpg`
- `berkeley-ai-hackathon.jpg`
- `streamlit-first-place.jpg`（PyCon 详情页第二张图与主页 Award）

主页小卡现在使用 3:4 竖向比例，并且整张卡片都可以点击进入对应的 Field Notes 详情页。详情页主图可保留原始比例，但若希望视觉更稳定，建议使用 16:9 或 3:2 横图。

## 4. 如果要调整裁切位置

这个静态 ZIP 已经为现有照片设置了合适的焦点。若只上传 GitHub Pages，最简单可靠的方法是在 Photoshop、Canva、Preview 或任意图片编辑器中先裁好，再覆盖同名文件。

如果你继续使用源码构建，裁切位置在 `app/data/field-notes.ts`：

- `homePosition`：主页 Field Notes 卡片焦点
- `coverPosition`：Field Notes 索引及详情主图焦点
- `images[].position`：详情页相册焦点

格式与 CSS `object-position` 相同，例如：`center 35%`、`left center`、`70% 40%`。

## 5. GitHub Pages 上传

把 ZIP 解压后，将解压目录里的全部文件上传到 GitHub Pages 所使用的仓库根目录。必须保留根目录的 `.nojekyll` 文件。主页文件是 `index.html`，不要额外套一层文件夹。
