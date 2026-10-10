# etf宣传gal demo

一个以 **ETF（交易型开放式指数基金）投资者教育** 为主题的视觉小说 demo，基于 [WebGAL](https://openwebgal.com) 引擎制作，导出为 Windows 桌面版（Electron，免安装）。

玩家扮演一名误入「幻境花园」的旅行者，由五位角色引导，从零开始理解 ETF 是什么、它和直接买股票有什么区别、以及它适合什么样的人。

---

## 一、项目概况

| 项目 | 说明 |
| --- | --- |
| 游戏名称 | etf宣传gal demo |
| 题材 | ETF 投资者教育 |
| 类型 | 视觉小说（AVG）／分支选项 |
| 引擎 | WebGAL（WebGAL Terre 导出） |
| 运行环境 | Windows x64 桌面版，免安装 |
| 当前篇幅 | 序章 + 第一章（demo 版） |
| 界面语言 | 简体中文 |
| 分支结构 | 有。选项采用汇流结构，不同分支最终回到同一收束点 |
| 流程图 | 已开启（`config.txt` 中 `Enable_flowchart:true`） |
| 游戏素材 | 背景 12 张、立绘 8 张、BGM 1 首、剧本 3 个文件 |

## 二、已完成的章节

- **序章「幻境花园」**：开场 → 五位角色登场 → 二选一（小白线 / 偏见线）→ 收束 → 进入第一章
- **第一章「数据街·茶饮站」（林晚路线）**：讲解恒生科技指数与恒生科技 ETF，3 组共 9 个选项 → 章末

其二至第六章（其余四位角色的个人线）尚未制作。

## 三、登场角色

| 角色 | 在 demo 中负责的内容 |
| --- | --- |
| 沈渡 | ETF 的定义、费率优势 |
| 季寻 | 串场引导，负责引入第一章 |
| 林晚 | 第一章主讲：恒生科技指数与恒生科技 ETF |
| 陈一苇 | 持仓透明度、行业性下行风险 |
| 顾泠 | 新手如何选择第一只 ETF |

---

## 四、怎么玩

### 方式一：Windows 桌面版（推荐）

> **不要直接下载 ZIP。** 本仓库的大文件用 Git LFS 托管，GitHub 生成的 ZIP 包里 `WebGAL.exe` 和 `resources/app.asar` 只是几十字节的指针文本，直接双击会启动失败。

1. 安装 [Git LFS](https://git-lfs.com)（每台机器只需一次）：
   ```
   git lfs install
   ```
2. 克隆仓库：
   ```
   git clone https://github.com/lzitong01-wq/etf-gal-demo.git
   cd etf-gal-demo
   ```
   如果之前已经克隆过、发现 `.exe` 只有 1 KB 左右，进入目录执行 `git lfs pull` 补拉真实文件即可。
3. 双击 **`WebGAL.exe`** 启动，不需要安装。
   首次运行若被杀毒软件拦截，是未签名 Electron 程序的常见误报，选择允许即可。
4. 标题页点击「开始游戏」。

### 方式二：在 macOS / Linux / 浏览器里玩

`WebGAL.exe` 只有 Windows 版。其他平台需要先把游戏资源从 Electron 包里取出来，再用 WebGAL 运行时打开：

1. 解包（需要 Node.js）：
   ```
   npx @electron/asar extract resources/app.asar ./app
   ```
   解出来的 **`app/public/game/`** 就是游戏本体。
2. 到 [WebGAL](https://openwebgal.com) 下载编辑器 WebGAL Terre，或使用其网页版运行时。
3. 把 `game/` 目录放进运行时的 `public/` 下，启动即可游玩。

### 游戏内操作

- **推进对话**：点击画面任意位置，或滚动鼠标滚轮
- **做出选择**：点击屏幕上出现的选项按钮（序章 1 组、第一章 3 组）
- **按钮栏**（鼠标移到画面底部呼出）：回想、流程图、重播、自动、快进、快速存档、快速读档、存档、读档、全屏、选项、标题
- **设置**（选项页）：
  - 系统：自动播放速度、快进模式（已读／全部）、语言、清除存档、导入导出存档
  - 显示：全屏模式、文字显示速度、文本大小、文本字体、文本框不透明度
  - 音频：主音量、语音音量、背景音乐音量、音效音量、UI 音效音量
- **流程图**：按钮栏的「流程图」可查看已走过的剧情节点
- **存档**：手动存档；「快速存档／快速读档」用于临时保存进度

---

## 五、仓库结构

```
.
├── WebGAL.exe              # Windows 启动程序（169 MB，Git LFS）
├── resources/
│   └── app.asar            # Electron 应用包，含引擎与游戏资源（84 MB，Git LFS）
├── locales/                # Chromium 语言资源（*.pak，Git LFS）
├── *.dll *.pak *.bin *.dat # Electron / Chromium 运行时（Git LFS）
├── LICENSE.electron.txt
├── LICENSES.chromium.html
├── .gitattributes          # Git LFS 规则
└── README.md
```

解包 `app.asar` 后的游戏本体位于 `public/game/`：

```
game/
├── config.txt              # 游戏名、标题图、标题 BGM、文本框主题、流程图开关
├── scene/
│   ├── start.txt           # 入口场景
│   ├── prologue.txt        # 序章「幻境花园」
│   └── chapter1.txt        # 第一章「数据街·茶饮站」
├── background/             # 背景图（序章 scene_0*.webp、第一章 1~4.webp）
├── figure/                 # 角色立绘
└── bgm/                    # 背景音乐 111.mp3
```

剧本为纯文本的 WebGAL 脚本，可直接用文本编辑器修改后重启游戏生效。

## 六、技术栈

- **WebGAL**：网页端视觉小说引擎，剧本使用 WebGAL 脚本语法（`changeBg` / `changeFigure` / `choose` / `label` / `jumpLabel` 等指令）
- **Electron**：桌面端打包，含 `steamworks.js`（Steam 成就接口预留，本 demo 未接入具体 App ID）
- 引擎部分沿用 WebGAL 的 MPL-2.0 许可；剧本、立绘、音乐为本项目原创内容

## 七、说明

- 本作是**投资者教育演示作品**，剧情对话仅用于普及 ETF 基础概念，**不构成任何投资建议**。
- 仓库约 336 MB，其中 `WebGAL.exe`（169 MB）与 `resources/app.asar`（84 MB）通过 Git LFS 托管，会占用 GitHub 账号的 LFS 存储与流量额度。
- 若只想获取游戏资源（约 6 MB）而非完整桌面版，克隆时可用：
  ```
  GIT_LFS_SKIP_SMUDGE=1 git clone https://github.com/lzitong01-wq/etf-gal-demo.git
  ```
  再按「方式二」解包取用。
