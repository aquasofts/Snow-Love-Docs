# 📜 Ren'Py 脚本基础指南

本文档旨在帮助没有编程基础的文案/策划人员快速上手，编写符合项目规范的剧情脚本。

## 1. 最基本的对话

在 Ren'Py 中，写对话非常简单，只需要 `角色代号 "台词内容"`。

```
# 例子：
m "（长春的风，似乎总比家乡来得更直爽一些。）"

# 素织说话
s "你走路不看路的吗？"

# 旁白（不加代号）
"我低下头，发现地上掉了一个精致的挂件。"
```

## 2. 显示画面 (Scene & Show)

- **`scene` (场景)**：切换大背景。这会清除之前所有的立绘。
- **`show` (立绘)**：在背景上叠加人物。
- **`hide` (隐藏)**：让人物消失。

```
# 1. 先切背景：操场
scene bg playground with fade

# 2. 显示素织在中间
show suzhi casual angry at center with dissolve

s "你撞到我了！"

# 3. 素织心情变好了 (直接 show 新表情，会自动替换旧表情)
show suzhi casual normal

s "算了，原谅你。"

# 4. 素织离开了
hide suzhi with easeoutright
```

## 3. 播放声音 (Audio)

请使用我们在 `script.rpy` 头部定义好的简写变量。

```
# 播放背景音乐 (BGM) - 循环播放
play music bgm_daily fadein 1.0

# 播放音效 (SE) - 只响一次
play sound se_bump

# 停止音乐
stop music fadeout 1.0
```

## 4. 转场效果 (Transitions)

为了让画面不生硬，我们在指令后面加 `with 效果名`。

- `with fade`：黑屏淡入淡出 (常用于切换大场景/时间流逝)。
- `with dissolve`：叠化 (常用于人物出现/表情切换)。
- `with vpunch`：剧烈震动 (常用于撞击/惊讶)。

```
# 例子：
scene bg dorm_room_morning with fade
"第二天早晨……"
```

## 5. 常用位置 (Transforms)

控制立绘在屏幕上的位置：

- `at center`：中间 (默认)
- `at left`：左边
- `at right`：右边
- `at truecenter`：正中间 (包括上下左右)