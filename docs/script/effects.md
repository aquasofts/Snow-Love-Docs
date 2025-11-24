# ✨ 特效指令大全

为了增强演出的动感（尤其是搞笑桥段），我们在 `script.rpy` 中预制了许多自定义特效。请直接复制以下代码使用。

## 1. 震动类 (Shakes)

用于表达撞击、惊讶、生气或混乱。

| 代码               | 说明                        | 适用场景                   |
| ------------------ | --------------------------- | -------------------------- |
| `with vpunch`      | **垂直剧烈震动** (系统自带) | 撞人、摔倒、震惊           |
| `with hpunch`      | **水平剧烈震动** (系统自带) | 被打脸、左右推搡           |
| `at soft_shake`    | **轻微持续晃动**            | 紧张发抖、素织害羞时的动摇 |
| `at running_shake` | **模拟跑步颠簸**            | 第一人称视角的奔跑场景     |

**使用示例：**

```
# 素织害羞得发抖
show suzhi casual shy at center, soft_shake

# 木子米狂奔
scene bg campus_road_blur at running_shake
```

## 2. 视觉类 (Visuals)

| 代码                 | 说明           | 适用场景                         |
| -------------------- | -------------- | -------------------------------- |
| `with flash`         | **白屏闪光**   | 回忆杀、被泼牛奶的瞬间、开悟     |
| `at slow_motion_pan` | **慢动作平移** | 关键道具（如牛奶）飞在空中的特写 |

**使用示例（草莓牛奶名场面）：**

```
# 牛奶飞出去了！慢动作！
show image_milk_splash at slow_motion_pan
with flash
```

## 3. Q版动画 (Chibi Animations)

这是第五章专用的“追逐战”特效，让 Q 版小人在屏幕上乱窜。

| 变换名 (Transform) | 效果描述                                         |
| ------------------ | ------------------------------------------------ |
| `panic_run_left`   | **慌张逃跑**：角色在右侧区域左右横跳并上下颠簸。 |
| `chase_run_left`   | **紧追不舍**：角色在更靠右的位置，动作更激进。   |
| `jump_attempt`     | **原地蹦跶**：白墨萱够书时的跳跃动作。           |

**使用示例（素织追杀木子米）：**

```
# 1. 隐藏正常立绘
hide suzhi
hide muzimi

# 2. 显示Q版小人动画
show sd_suzhi_run at chase_run_left
show sd_muzimi_run at panic_run_left

s "给我站住！！！"
m "救命啊！！！"
```