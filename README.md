# 小书桌 · 一年级学习站

面向小学一年级（6~7 岁）的科普与思维课程合集，纯静态页面，GitHub Pages 托管。

## 📚 页面列表

| 页面 | 文件 | 内容 |
| --- | --- | --- |
| 🗂️ **导航首页** | [index.html](./index.html) | 全部课程入口 |
| 🔬 小学一年级科普教程 | [kexue.html](./kexue.html) | 6 大领域拆成 30 周，每周一个主题 + 动画演示 + 动手实验 |
| 🧠 一年级思维课堂 | [siwei.html](./siwei.html) | 6 大思维模块 + 8 关互动闯关游戏 |
| ⚫ 五子棋成长课 | [wuziqi.html](./wuziqi.html) | 6 级 30 课 + 九种棋型图鉴 + 10 关实战 + 人机对弈 |
| ⚪ 围棋启蒙课 | [weiqi.html](./weiqi.html) | 从吃子到围空的启蒙路径 |

> 注：原先科普教程占用 `index.html`，现已让位给导航页，改名为 `kexue.html`。旧链接不会 404，只会落到导航页。

## ➕ 新增一个页面

1. 把新的 `xxx.html` 放到仓库根目录。
2. 打开 `index.html`，在底部 `<script>` 里的 **`PAGES` 数组**追加一项：

```js
{
  href:'xxx.html',
  emoji:'🎨',              // 封面大图标
  mini:['✏️','🌈'],        // 封面角落的两个小图标
  color:'#2FC79A',         // 封面底色（建议用下方色板）
  title:'页面标题',
  desc:'一两句话介绍。',
  facts:[['6','大模块'],['20','分钟/节']],   // 卡片上的数据标签
  badge:'NEW'              // 右上角徽章，不需要就留空字符串 ''
}
```

3. 在新页面顶部加一个返回入口，指向 `index.html`（参考 `siwei.html` 的 `.home-btn`）。
4. 更新上面的页面列表表格。

卡片是数据驱动渲染的，**不用改 HTML 结构**，只改数组即可。

## 🎨 色板

| 变量 | 色值 | |
| --- | --- | --- |
| tomato | `#FF5B4A` | 番茄红 |
| sun | `#FFC53D` | 柠檬黄 |
| mint | `#2FC79A` | 薄荷绿 |
| sky | `#4E9CFF` | 天空蓝 |
| grape | `#A374FF` | 葡萄紫 |
| bubble | `#FF8FB1` | 泡泡粉 |
| ink | `#2A211C` | 描边墨色 |
| paper | `#FFF4DF` | 奶油纸 |

## 🛠️ 说明

- 所有页面都是**单文件 HTML**，无构建步骤、无依赖，双击即可本地预览。
- 字体走 Google Fonts（站酷快乐体 + Fredoka），断网时自动降级为系统圆体，不影响阅读。
- `.nojekyll` 用于关闭 GitHub Pages 的 Jekyll 处理。

## ⚙️ kexue.html 的例外：由脚本生成

科普教程是唯一**不要直接手改**的页面 —— 它由 `~/Work/kexue-build/` 下的脚本拼装：

| 文件 | 作用 |
| --- | --- |
| `kexue_backup.html` | 改版前的原始教案，是全部课文的唯一来源 |
| `extract_kexue.py` | 从原始教案切出 30 课 + 模块简介 → `kexue_data.json` |
| `kexue_shell.html` | 页面外壳：样式、侧栏、路由，含 `<!--WEEKS-->` 等占位符 |
| `kexue_anims.js` | 动画引擎 + 各周动画（目前第 1~5 周） |
| `build_kexue.py` | 注入并输出到 `deploy-site/kexue.html`，自带校验 |

改样式改 `kexue_shell.html`，加动画改 `kexue_anims.js`，然后：

```bash
cd ~/Work/kexue-build && python3 build_kexue.py
```

第 6~30 周目前是「动画演示制作中」占位，在 `kexue_anims.js` 里补 `ANIMS[n]`、
并在 `build_kexue.py` 的 `ANIM_TITLES` 里加一行标题，重新构建即可点亮。
