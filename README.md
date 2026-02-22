# Vela数字华容道 (Number Sliding Puzzle) - Smartwatch

一款专为智能手表和手环开发的数字华容道游戏。本项目基于 **Vela JS / 快应用 (Quick App)** 框架开发，深度适配了圆形表盘与矩形宽屏设备，并集成了陀螺仪体感等多种硬核操作交互方式。

## 🛠️ 技术栈 (Tech Stack)

* **框架:** Vela JS / Quick App (快应用)
* **语言:** 视图层 (HTML/Template) + 样式层 (CSS/LESS) + 逻辑层 (JavaScript)
* **核心系统 API:** `@system.router`, `@system.storage`, `@system.sensor`, `@system.brightness`

## ✨ 技术特性 (Technical Highlights)

### 1. 多模态交互系统 (Multi-modal Interaction)

针对智能穿戴设备的屏幕尺寸限制，项目摒弃了单一的触控，实现了三种独立的操作逻辑：

* **点触移动 (Click):** 基于坐标系计算相邻矩阵，精准判断合法移动步数。
* **滑动操作 (Swipe):** 监听 `@touchstart` 与 `@touchend`，通过计算 `deltaX` 和 `deltaY` 的向量差，自定义灵敏度阈值 (`SWIPE_THRESHOLD`)，实现了防误触的滑动方向判定。
* **陀螺仪体感 (Gyroscope):** 接入底层 `@system.sensor` 加速度计，每 500ms 截取一次三轴数据，将手腕的物理倾斜转化为游戏内方块的滑动。开启陀螺仪模式时，自动调用 `@system.brightness.setKeepScreenOn` 保持屏幕常亮，优化体感游戏体验。

### 2. 响应式与跨设备适配 (Responsive UI for Wearables)

通过 CSS Media Queries 完美兼容不同形态的智能设备：

* **圆形表盘设备** (如 Watch S4, 466x466): 触发 `@media (shape: circle)`，重构安全区域 (Safe Area)，调整字体、边距以及操作面板的圆角。
* **矩形宽屏设备** (如 手环9 Pro, 336x480): 触发 `@media (min-width: 150) and (shape: rect)`，最大化利用屏幕显示面积，提供更舒展的布局。

### 3. 高性能动画与渲染 (Animation & Rendering)

* **入场级联动画:** 不依赖繁重的 CSS 动画库，完全使用纯 JavaScript 的时间戳 (Date.now) 和递归调用模拟 `requestAnimationFrame`，配合 Ease-Out 缓动函数，实现了菜单列表带有 Stagger (错开) 效果的丝滑滑入动画。
* **自定义字体** 

### 4. 核心算法与状态管理 (Algorithm & State Management)

* **可解性布局生成:** 为了保证生成的 3x3, 4x4, 5x5 棋盘绝对有解，摒弃了简单的纯随机打乱，采用了“逆向移动法”：从初始完成状态开始，随机移动空白块 200 倍于网格尺寸的次数，确保生成的每一局都是有效游戏。
* **本地数据持久化:** 采用 `@system.storage` 异步存储不同难度下的“最优步数”与“最短时间”，并实现 JSON 格式的安全序列化与反序列化解析。

## 📂 项目结构 (Project Structure)

```text
├── common/                  # 公共资源目录 (图片、字体、音频等)
│   ├── data/
│   │   └── yuanfont.ttf     # 数字展示定制字体
│   └── exit.png  ...        # UI 图标资源太多了懒得写
├── pages/                   # 页面视图目录
│   ├── index/               # 游戏主引导页
│   │   ├── index.ux         
│   ├── game/                # 游戏主页及核心逻辑
│   │   ├── game.ux          
│   ├── login/               # 启动界面
│   │   ├── login.ux         
│   ├── about/               # 关于界面
│   │   ├── about.ux         
│   └── lsjl/                # 历史成绩页面
├── manifest.json            # 运用配置、权限声明 (sensor, storage等)
└── README.md

```

## 🚀 本地运行与调试 (Getting Started)

1. 请确保已安装快应用 IDE 或目标穿戴设备的开发者调试工具。
2. 克隆本项目：
```bash
git clone https://github.com/jinmohan/Number-Sliding-Puzzle.git

```


3. 在 IDE 中打开项目根目录，安装相关依赖并编译。

## 📄 开源协议 (License)

本项目遵循 [Apache-2.0 License](http://www.apache.org/licenses/) 开源协议。欢迎 Fork 学习与提交 PR 改进！

---


# Develop By: MatrixFive Studio
![MatrixFive Studio](https://mfis.one/heartrate/MatrixFiveStudio.png "MatrixFive Studio")

---
