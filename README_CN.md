# Arcade Manifold

[English](README.md) | [中文](README_CN.md)

![装在 32HP 木盒里的 Arcade Manifold](docs/images/01-finished-module.jpg)

**Arcade Manifold** 是由 [Meng Qi（孟奇）](https://www.mengqimusic.com) 设计的 32HP 无源 4 通道 Eurorack 模块。它可以作为信号路由器、瞬时开关、无源混音器、信号复分器（Multiple）与多规格格式转换器使用，围绕手感干脆的 SANWA 街机按钮打造，适合快速、直接的现场演奏。

整套电路完全无源，无需接入电源，既可以直接装入不供电的控制器小盒，也可以放进 32HP 独立木盒中使用。

---

## 功能与面板说明

模块由 **4 个完全相同的纵向通道** 组成，面板顶部中央另设有一个 **接地香蕉座**，用于与 Buchla、Serge、Ciat-Lonbarde 等香蕉插口系统建立共地连接。

每个通道从上到下印有四个中文标识：

| 标识 | 含义 | 对应接口 / 控件 |
| :---: | :--- | :--- |
| **出** | 输出（Output） | 6.35 mm（大二芯）、3.5 mm（小二芯）与 4 mm 香蕉插口 |
| **入** | 输入（Input） | 6.35 mm（大二芯）、3.5 mm（小二芯）与 4 mm 香蕉插口 |
| **门** | 开关模式（Mode） | DPDT 拨动开关：切换 **常开**（按下按钮导通）或 **常闭**（平时直通，按下按钮切断） |
| **力** | 触发演奏（Action） | **SANWA OBSF-24** 24 mm 街机按钮 |

### 现场路由与混音玩法

配合可叠插香蕉线，你可以随时改变信号流向：

- **输入端预混音**：在「入」区用香蕉线把多路信号叠插混合，再通过各通道的街机按钮把混合信号切分、路由到不同输出。
- **输出端后混音**：在「出」区用香蕉线把多个通道的输出并在一起，用街机按钮实时决定哪些信号进入最终混音。
- **跨格式跳线**：同一通道内同时提供 3.5 mm、6.35 mm 与 4 mm 香蕉口，可在 Eurorack、吉他效果器/乐器与香蕉模块之间自由转接。
- **多台串联**：多台 Arcade Manifold 可通过香蕉线与顶部接地口自由互联，且全部无需供电。

---

## 电路简述

每个通道使用一块独立 **Core PCB**，垂直安装在 **Faceplate PCB** 背面。

- 每块 Core PCB 上有 **3 颗 5.1 kΩ（1206）贴片电阻**（4 通道总计 **12 颗**）：
  1. 输入 6.35 mm / 3.5 mm 插座与输入香蕉焊盘（`Nana`）之间
  2. 输入香蕉焊盘（`Nana`）与开关/按钮输入端之间
  3. 开关输出端与输出总线（`Nana` / 3.5 mm / 6.35 mm）之间
- **常开模式**：松开按钮时输入与输出断开，按下按钮导通。
- **常闭模式**：松开按钮时信号直通，按下按钮将内部开关节点拉低到地；串联的 5.1 kΩ 电阻既保证无源混音隔离，也避免外部信号源或输出混音总线被直接对地短路。

---

## 仓库目录

```text
Arcade-Manifold/
├── README.md                                 # 英文说明文档（主文档）
├── README_CN.md                              # 中文说明文档
├── LICENSE                                   # MIT 开源协议
├── docs/
│   ├── diy-guide.md                          # 英文 DIY 组装指南
│   ├── diy-guide_CN.md                       # 中文 DIY 组装指南
│   └── images/                               # 组装实拍图与木盒图纸预览
└── hardware/
    ├── BOM.csv                               # 完整元件清单
    ├── core/
    │   ├── AM_Core_Gerbers.zip               # Core PCB 打样 Gerber 压缩包（需 4 块）
    │   ├── Arcade Manifold.lay6              # Sprint-Layout 6 源文件
    │   └── gerbers/                          # 解压后的 Gerber 与钻孔文件
    ├── faceplate/
    │   ├── AM_Faceplate_Gerbers.zip          # Faceplate PCB 打样 Gerber 压缩包（需 1 块）
    │   ├── AM Faceplate.lay6                 # Sprint-Layout 6 源文件
    │   └── gerbers/                          # 解压后的 Gerber 与钻孔文件
    └── enclosure/
        └── AM_Box_32HP.ai                    # 32HP 木盒加工图纸（Illustrator / PDF）
```

---

## 元件清单（BOM）

完整表格文件：[`hardware/BOM.csv`](hardware/BOM.csv)

| 元件 | 品牌 / 型号 | 数量 | 说明 |
| :--- | :--- | :---: | :--- |
| Core PCB（核心板） | 定制（`AM Core`） | 4 | 80.96 × 22.86 mm，双层，1.6 mm FR4（每通道 1 块） |
| Faceplate PCB（面板） | 定制（`AM Faceplate`） | 1 | 162.5 × 128.7 mm（32HP × 3U），双层，1.6 mm FR4 |
| 5.1 kΩ 贴片电阻（1206） | 通用（`5K1 1206`） | 12 | 每块 Core PCB 3 处焊盘全部焊 5.1 kΩ（4 × 3 = 12） |
| 24 mm 街机按钮 | **SANWA** `OBSF-24` | 4 | 卡扣式安装，每通道 1 颗 |
| 迷你 DPDT 拨动开关（ON-ON） | **德利威（Dailywell）** `2MD1T2B2M7QE` | 4 | 弯脚直插（Vertical Right-Angle），每通道 1 颗 |
| 6.35 mm 卧式 PCB 母座 | **Neutrik（甬声）** `YS-215A` | 8 | 每块 Core PCB 2 个（输入 / 输出） |
| 3.5 mm 卧式 PCB 母座 | 通用 `PJ-313` | 8 | 每块 Core PCB 2 个（输入 / 输出） |
| 4 mm 面板安装香蕉座 | **RCI** `R1-16A` | 9 | 8 个通道信号座（如蓝色）+ 1 个顶部中央接地座（如黑色） |
| 裸铜线 / 镀锡单芯硬导线 | 通用 | 若干 | 线径约 0.5–0.8 mm，用于按钮、香蕉座与顶部接地座飞线 |
| 32HP 木盒（可选） | 定制 | 1 | 若装入 Eurorack 机箱则无需木盒 |

*可选配件*：可叠插 4 mm 香蕉跳线（原版成品附带 5 根），以及 4 颗 M3 面板固定螺丝（木盒版可用自攻木螺丝）。

---

## PCB 打样说明

两块电路板均使用 **Sprint-Layout 6**（`.lay6`）绘制，仓库内已准备好可直接上传板厂的 Gerber 压缩包：

- **Core PCB** — [`hardware/core/AM_Core_Gerbers.zip`](hardware/core/AM_Core_Gerbers.zip)
  - 尺寸：`80.96 × 22.86 mm`，双层板，板厚 `1.6 mm` FR4
  - 需求数量：**每台 4 块**（板厂常见起订量 5 片，刚好留 1 片备用）
- **Faceplate PCB** — [`hardware/faceplate/AM_Faceplate_Gerbers.zip`](hardware/faceplate/AM_Faceplate_Gerbers.zip)
  - 尺寸：`162.5 × 128.7 mm`（32HP × 3U），双层板，板厚 `1.6 mm` FR4
  - 需求数量：**每台 1 块**
  - 工艺：正面字符（**出 / 入 / 门 / 力**、莲花标）与孔位装饰环均采用阻焊开窗露铜设计，**蓝油 + 喷锡或沉金** 可还原原版视觉。
  - 结构细节：四角采用 `5.2 × 3.2 mm` 标准 Eurorack 腰型安装槽孔，9 个香蕉座孔位带双平边防转铣槽（适配 `RCI R1-16A`）。

---

## 组装指南

详细图文组装步骤与装机后万用表自检方法见 **[`docs/diy-guide_CN.md`](docs/diy-guide_CN.md)**。

---

## 可选 32HP 木盒图纸

加工源文件：[`hardware/enclosure/AM_Box_32HP.ai`](hardware/enclosure/AM_Box_32HP.ai)（内含完整 PDF 数据流，可直接用任意 PDF 阅读器打开查看矢量图）。

![32HP 木盒加工图纸预览](docs/images/05-enclosure-drawing.png)

> **图纸注意**：画板里上下共画了两个木盒，**制作 Arcade Manifold 请看上方 `183 × 149 × 52 mm` 的图纸**。下方 `173 mm` 带侧面圆孔的盒子属于另一款 30HP 模块，请直接忽略。

**32HP 木盒参数（上方图纸）：**
- 外径：`183 × 149 × 52 mm`（无盖 5 面盒）
- 内径：`163 × 129 mm`，内深 `42 mm`
- 板材与工艺：四周为 `10 mm` 厚辐射松、底板为 `10 mm` 集成材（底面雕刻莲花标），表面深度碳化
- 内侧安装支条（图中绿色）：厚 `8 mm`、高 `40 mm`（比盒口低 `2 mm`，拧上面板后恰好与盒沿齐平）

---

## 开源协议

本项目基于 [MIT License](LICENSE) 开源。请自行评估并承担制作与使用这些硬件文件的风险。
