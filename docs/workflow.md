# 【教程】从零开始：如何利用AI协助制作我们的Galgame项目

大家好！这是我们要制作的Galgame项目的开发手册。

为了加快开发进度，我们决定采用 **“AI辅助工作流”**。无论你是没有任何绘画基础的纯新手，还是不懂代码的剧情策划，只要按照这份文档操作，你就能成为我们项目的核心开发者！

我们的目标是制作一款以校园生活为背景（参考脚本中的长春工程学院设定）的视觉小说。

## 第一部分：背景图制作 (实景转二次元)

我们的背景图追求“写实风格的二次元化”。因为故事发生在现实原型的校园里，我们采用 **“实拍照片 + AI 重绘”** 的方式。

### 1. 准备工作

- **工具**：Stable Diffusion WebUI (推荐) 或 Midjourney。
- **素材**：一张构图清晰的实拍照片（例如：学校操场、宿舍、食堂）。

### 2. 操作流程 (以 Stable Diffusion 为例)

我们使用 **图生图 (Img2Img)** 功能。

1. **上传图片**：在“图生图”界面上传你的实拍照片。
2. **设置重绘幅度 (Denoising Strength)**：**这是最关键的参数！**
   - 设置为 `0.3` - `0.4`：保留原有建筑结构和细节，仅改变画风（推荐）。
   - 设置为 `0.5` 以上：AI 会开始乱改建筑结构（除非照片太模糊，否则不建议）。
3. **启用 ControlNet (神器)**：
   - 如果你希望线条完全对齐（比如窗户、跑道线），请开启 `ControlNet`。
   - **Preprocessor (预处理器)** 选 `Canny` (边缘检测) 或 `Lineart`。
   - **Model (模型)** 选对应的 `control_v11...canny` 等。
   - 这能像描图纸一样锁死结构。

### 3. 提示词 (Prompts) 参考

请复制以下提示词，并根据场景微调：

**正向提示词 (Positive Prompts):**

```
(masterpiece, best quality:1.2), makoto shinkai style, anime background, scenic, 
school life, bright sunlight, blue sky, clouds, highly detailed, 4k, 
no humans, (outdoors:1.2)
```

*注：如果是室内，把 `outdoors` 改为 `indoors`, `room` 等。*

**反向提示词 (Negative Prompts):**

```
(worst quality, low quality:1.4), text, watermark, humans, people, distorted structures, blurry
```

### 4. 实战案例

比如我们项目中的 `bg playground.jpg`，就是通过这种方式，将真实的塑胶跑道照片转化为了新海诚风格的动漫背景。

## 第二部分：角色立绘制作 (保持角色一致性)

这是最难的部分。我们需要生成像“素织”或“木子米”这样画风统一的角色，并制作不同的表情（差分）。

### 1. 风格设定 (Style)

我们的项目采用 **“日系赛璐璐 (Cel Shaded)”** 或 **“精致插画风”**。

- **大模型 (Checkpoint)** 推荐：`Anything V5`, `Counterfeit V3`, 或 `MeinaMix`。

### 2. 核心咒语 (Prompts)

为了保证角色长相不乱变，必须固定描述词。

**以“素织”为例的固定提示词：**

```
1girl, solo, silver hair, long hair, green eyes, flower hair ornament, 
knitted sweater, plaid skirt, holding a book, gentle smile, 
(anime style:1.2), flat color, soft lighting, white background, simple background
```

### 3. 如何制作“表情差分” (同一个动作，不同表情)

在 Galgame 中，我们需要 `normal` (正常), `angry` (生气), `shy` (害羞) 等表情。

**方法：使用“局部重绘 (Inpaint)”**

1. 生成一张满意的基础立绘（例如：`suzhi casual normal`）。
2. 发送到 **Inpaint** 页面。
3. 用画笔涂黑**面部区域**（眼睛、眉毛、嘴巴）。
4. **修改提示词**：
   - 生气：`angry, frowning, narrowed eyes`
   - 害羞：`blush, shy, embarrassed, looking away`
   - 惊讶：`open mouth, wide eyes, surprised`
5. 点击生成。这样身体和衣服完全不会变，只有表情变了！

### 4. 如何利用图生图优化手绘草图

如果你会画火柴人，也可以用 AI 细化。

- 画出角色的动作火柴人。
- 放入 **Img2Img**。
- 配合 `ControlNet OpenPose`（姿态控制）。
- 输入上述的角色提示词，AI 就会根据你的骨架生成精美立绘。

## 第三部分：利用 AI 辅助编写 Ren'Py 代码

我们的项目运行在 Ren'Py 引擎上。你不需要精通 Python，让 ChatGPT/Claude 来帮你写！

### 1. 喂给 AI “上下文”

直接让 AI 写代码容易出错，你必须先告诉它我们定义了哪些角色。

**请把这段话发给 AI (基于我们的 `script.rpy`)：**

> “我正在制作一个 Ren'Py 游戏。这是我的角色定义代码，请记住这些变量： `define m = Character("木子米", color="#4db6ac")` `define s = Character("素织", color="#ef5350")` `define l = Character("凌宁", color="#81d4fa")` `define e = Character("空军少尉", color="#1a237e")` 同时我有一些自定义变换，比如 `vpunch` (震动) 和 `slow_motion_pan`。”

### 2. 让 AI 续写剧情代码

当你卡文或者不想写格式时，发送指令：

**指令示例：**

> “请帮我写一段代码。场景是 `bg playground`。 剧情内容：素织（s）正在生气，因为木子米（m）迟到了。 要求：
>
> 1. 先播放背景音乐 `audio.bgm_daily`。
> 2. 木子米从左边慌张地跑进来（使用 `moveinleft`）。
> 3. 素织显示生气的立绘 `suzhi casual angry`，并使用 `vpunch` 震动效果表现她的愤怒。
> 4. 对话要有趣一点。”

**AI 会生成类似这样的可用代码：**

```
label running_late_event:
    scene bg playground with fade
    play music bgm_daily fadein 1.0

    # 木子米慌张入场
    show lingning casual run at left with moveinleft
    
    m "呼……呼……抱歉！闹钟坏了！"

    # 素织生气震动
    show suzhi casual angry at center with vpunch
    
    s "现在的闹钟还会自己关机吗？木子米！"
    s "全班都在等你去搬书呢！"
    
    m "下次一定不敢了……"
```

## 第四部分：重要注意事项 (避坑指南)

### 1. 永远的痛：AI 画手

- **问题**：AI 经常把手画成 6 根手指或一团面条。
- **解决**：
  - 尽量生成半身像，把手切在画面外。
  - 如果必须露手，使用 `ControlNet Depth` 找一张真人的手做参考。
  - 或者后期用 PS 涂改一下手指。

### 2. 文件命名规范 (非常重要！)

Ren'Py 依靠文件名来识别图片。请严格遵守以下格式，AI 生成图片后手动重命名：

- **背景**：`bg 场景名.jpg` (例如：`bg library.jpg`)
- **角色**：`角色名 服装 表情.png` (例如：`suzhi camo smile.png`)
  - 注意：必须全小写，用空格隔开。不要用中文文件名！

### 3. 图片尺寸

- 我们项目的标准分辨率是 **1920x1080**。
- 生成的背景图如果不够大，请使用 AI 的 **"Upscale (高清放大)"** 功能，不要直接拉伸，会糊。

### 4. 抠图

- AI 生成的角色图是有背景的。
- 推荐使用 `Remove.bg` 或 Photoshop 的“一键移除背景”功能，将立绘处理成透明背景的 PNG 格式，再放入游戏文件夹。

**结语**

AI 是我们的画笔，也是我们的键盘。希望大家利用好这些工具，让我们一起把《长春工程学院雪之恋》做出来！如果有任何技术问题，请在群里@我。