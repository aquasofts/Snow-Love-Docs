# 🌸 素织 (Suzhi)

> “啧，看在你态度诚恳的份上。这可是限量版的。”

## 🎭 人设基础

- **身份**：土木工程系新生，军训女生方队排头兵。
- **性格**：傲娇 (Tsundere)、要强、认真、但在熟悉的人面前会流露温柔。
- **外貌特征**：
  - **发色**：青蓝色/浅蓝色 (Cyan/Light Blue)
  - **瞳色**：翠绿色 (Green)
  - **发型**：平时披发带花朵发饰，军训时扎马尾。
  - **关键道具**：书籍、草莓牛奶（孽缘）。

## 🎨 AI 绘画咒语 (Prompts)

为了保持画风统一，生成素织的立绘或CG时，请**务必**包含以下核心词条。建议配合 ControlNet 使用。

**基础特征 (Base):**

```
1girl, solo, light blue hair, long hair, green eyes, hair flower, flower ornament, delicate face, (anime style:1.2), flat color, cel shading
```

**服装差分 (Outfits):**

 **便服 (Casual)** - 参考样图" **描述**：米白色针织衫，格子裙，文学少女风。 `text white knitted sweater, plaid skirt, holding a book, gentle expression, upper body `

**迷彩服 (Camo)** - 军训篇" **描述**：中国大学军训迷彩服。 `text military camouflage jacket, military camouflage pants, ponytail, serious expression, outdoors, school playground background `

**湿身/狼狈 (Wet)** - 草莓牛奶事件" **描述**：被牛奶泼到，脸上和衣服有污渍。 `text white shirt, stained clothes, messy hair, pink liquid stain on face, blush, shy, embarrassed, arms crossed, angry `

## 🖼️ 素材列表 (Assets)

在 `script.rpy` 中已定义的立绘状态：

| 状态关键词 | 对应代码示例                | 说明                       |
| ---------- | --------------------------- | -------------------------- |
| **正常**   | `show suzhi casual normal`  | 平时对话                   |
| **生气**   | `show suzhi casual angry`   | 骂木子米时用               |
| **害羞**   | `show suzhi casual shy`     | 被调侃时用                 |
| **看书**   | `show suzhi casual reading` | 图书馆/教室静止状态        |
| **迷彩服** | `show suzhi camo default`   | 军训期间通用               |
| **狼狈**   | `show suzhi casual wet`     | **名场面**：被泼牛奶后     |
| **衬衫**   | `show suzhi shirt shy`      | **福利**：洗衣服时脱掉外套 |

!!! note "立绘位置" 所有素织的立绘文件应存放在：`images/char/suzhi/` 目录下。