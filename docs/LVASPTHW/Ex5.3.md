# Ex5.3 最新更新内容

本节主要记录 p4vasp 的更新历史。

## 2026-11-24 更新内容：

1） Surface 来源下拉框改成一排三个按钮（Metal preset、Use bulk result、Open POSCAR/CIF），当前来源高亮。

2） 修复 Use bulk result 后晶格参数仍显示旧预设值的问题，改显示导入 Bulk 的实际 name/a/c。

3） 打包了新的 Windows 便携版（2026-11-24，源 42b9802a），含 Surface 来源按钮和 Bulk 晶格显示修复。

## 2026-11-23 更新内容：

1） DOS 轨道选择改多选组合（d 与分量互斥，分量可多选），Export scripts 同时生成 .py/.sh，新增无界面 DOS 分析命令。

2） Surface 保存时自动生成 rebuild_surface.py/.sh 重建脚本。

3） 移除 Surface 初始说明；d-band filling 单位统一标 a.u.；DOS 结果数值固定三位小数。

4） DOS 分析扩展到 s/p/d/f 全壳层，三排轨道按钮，按钮改名 Analyze DOS。

5） Windows 科学 worker 加入 pymatgen。

6） 打包了新的 Windows 便携版（2026-11-23，源 5ca60f29），含 Surface 重建、s/p/d/f 分析和无界面重放。

## 2026-11-22 更新内容：

1） Models 新增 ASE Surface 表面建模首版（fcc/bcc/hcp 模板、晶面指数、层数、真空、底部固定，存 POSCAR + surface.json）。

2） Slab 新增 Center/Bottom 摆放按钮（居中或底部留 0.1 Å）。

3） 个人元素资料改存 ~/.p4vasp/resources/（periodic.json、incar.json），git 更新不丢改动。

4） 新增可选 pymatgen 安装入口（install/install-pymatgen.sh，独立 .venv-pymatgen）。

5） ASE/RDKit/pymatgen 统一进 .venv-science 科学环境。

6） DOS 新增 pymatgen 分析（元素/原子、d 轨道、自旋、E−EF 窗口，输出 center/width/filling/Hilbert 上沿/D_d(EF)，可导 CSV），左右分栏默认显示。

7） 修复最大化/切换选项后 DOS 重绘不同步；Hilbert 输入支持舍入网格插值。

8） 分析摘要精简（标题带 pymatgen 版本），Cancel 改成 Export Python script，可导出独立重跑脚本。

9） 删除费米能级处 d-DOS（D_d(EF)）结果项，只留四项。

10） 能量范围改单行显示，自旋选择改 Both/Up/Down 三按钮。

## 2026-11-21 更新内容：

1） Control/Show 实时绘制细节降到约 70%（原生分段 32 改 22），交互更流畅，导出画质不变。

2） OUTCAR-* 文件名支持补齐（OUTCAR-freq、OUTCAR-frequency 及混合大小写走频率读取）。

3） 打包了新的 Windows 便携版（2026-11-21，源 f5de130e）。

## 2026-11-17 更新内容：

1） 振动预览鼠标导航对齐 Show（中键平移、右键缩放、Ctrl 左键旋转，播放/切换模式保留相机）。

2） 氢原子显示球半径放大 1.5 倍（只作用于 H）。

3） OUTCAR_freq 等频率文件名现在能直接打开（OUTCAR_* 不区分大小写走频率读取）。

## 2026-11-14 更新内容：

1） 做了 Python2 旧代码和依赖全盘审计（只出文档不删代码），新增依赖清单和版本快照工具。

2） 打了可运行基线检查点（标签 checkpoint/2026-11-14-before-legacy-interface-fixes），开始分批修旧接口：线程状态、VAC 计时、FFT/滤波、绘图值比较、PS/EPS/PDF、FIG/SVG 导出。

3） Resources 与旧 SQL 解耦（延迟加载），历史构建入口加保护，删了退役的三个旧 Makefile 和 44 个旧 Glade 1 资源文件。

4） Models 标签改按需加载，构造时间约少 61%。

5） 新增 Edit → Copy for ChatGPT…，可复制结构摘要（默认不含坐标），完整 POSCAR/INCAR 可选。

6） 打包了新的 Windows 便携版（2026-11-14，源 58e353dc），含 EXE、ZIP 及校验文件。

## 2026-11-13 更新内容：

1） XDATCAR 现在能在 Control 里按完整轨迹播放（以前只读单个结构），支持 Direct/Cartesian、VASP4/5 文件头及变胞，坏帧明确拒绝。

2） Linux 实测通过 71 原子、1000 帧的用户 XDATCAR。

## 2026-11-12 更新内容：

1） 整理了 10 月 29 日至 11 月 12 日的半月更新总结（28 项），保存到 Windows 桌面，不纳入 Git。

2） 打包了新的 Windows 便携版（2026-11-12，源 4add6800），含 EXE、ZIP 及校验文件。

## 2026-11-11 更新内容：

1） 修复了 macOS 上 Database → Resources 点击崩溃的问题，重启即可生效。

2） Resources 页签改名叫 Help and Support，图片统一放到 figures/ 目录，新增大师兄科研群-V（群号 1012023869）。

3） 每日名言从 12 条中文扩到 16 条，中英文轮换（新增 4 条英文，Emerson、Shakespeare），16 天循环。

## 2026-11-10 更新内容：

1） 打包了新的 Windows 便携版（2026-11-10，源 0ed090d7），包含最新频率布局、单元格复制、离子能量读取修复和 Get Thermochemistry 按钮。

## 2026-11-09 更新内容：

1） 左侧九个按钮和图标统一成同样大小。

2） 频率页面改成三行两列等宽布局。

3） 热化学表格四列共用剩余宽度，表头改单行，点击结果单元格可复制数值。

4） 修正了离子步能量误读未收敛电子迭代值的问题，改读正式离子步的 sigma->0 能量。

5） “Calculate correction”按钮改名叫“Get Thermochemistry”。

## 2026-11-08 更新内容：

1） Show 原生显示更平滑：晶胞线默认 2 像素改 1 像素，抗锯齿和光照调柔。

2） 热化学结果卡片精简：标题带 ASE 版本号，模式/波数移到结构预览左上角。

3） 导出位移 POSCAR 时自动保留固定标记，无来源时直接导出，不再弹窗确认。

4） 频率文件默认自动填第一个离子步的 E，E 右侧可另选 OUTCAR 读最后一步。

5） 能量表改成四列：项目/公式/eV 值/kJ/mol 值，校正行加粗。

## 2026-11-07 更新内容：

1） `p4v test.xyz` 等命令和 File/Open 现在能通过 ASE 导入非 VASP 结构（xyz、cif、pdb 等），无晶胞时两侧各加 10 Å。

2） 新增 Vibrations 振动分析：左侧按钮和 Analysis 菜单，可看频率、播模式动画、沿虚频位移导出 POSCAR，还能算热力学矫正（F/G）。

3） 修复了频率文件窗口（Open frequency OUTCAR 等）按钮看不见的问题，改用紧凑对话框，底部保留 Open/Save/Cancel。

4） 新增 Help → Acknowledgment 致谢表，含日期列，按日期升序排列。

5） 安装器改进：结束提示改英文，自动配置 p4v 别名，支持 `source install.sh` 装完自动加载，末尾附常用命令示例。

6） 安装器改回统一用 `bash install.sh`（撤回了 `source install.sh` 自动加载），用法示例移入 usage_commands.md。

7） 打包了包含 ASE/RDKit 的 Windows EXE（2026-11-07，源 a201929），放进 Downloads，双击即用。

8） 气相热力学改用参数弹窗（可改温度/压力），结果可另存 JSON + 独立重跑脚本。

9） 能读 R25 这类低输出级别的频率 OUTCAR（NWRITE=0 缺质量信息也能读）。

10） 实频下限固定 50 cm⁻¹，虚频一律排除，不再手动设 floor/tolerance。

11） 频率界面自适应布局：删除 Thermo 列，新增 Cell 开关和 X/Y/Z 重复数，Scale 右置，热力学结果卡片默认展开。

## 2026-10-07 更新内容：

1） 修复了 Mac 上通过 `p4v` 命令打开软件时界面藏在其他页面后面的问题。

以前在 Mac 上敲 `p4v`，界面弹出来了，但是藏在别的窗口后面，会让人误以为没打开。修完之后，界面会直接弹到最前面来。

2） 通过引入 ASE，完善了 Models 中 Bulk 的构建。以前 Models 里建 Bulk 不太顺手，现在调了 ASE 来帮忙，建起来更完整了。

3） 在 p4vasp 页面的底部添加了每日的名言警句：每天打开看到一句不一样的话。这个功能就是图个乐子。

4） 修复了 DOSCAR 可视化时，XY 轴数字的小数点问题。以前 DOSCAR 图上 XY 轴的数字小数点显示不对，看着别扭，现在修好了。

5） 制备了最新的 Windows EXE 版本，该版本中可以直接调用 内置的ASE 去实现 Bulk 的构建，以及调用 RDKIT 去实现分子模型的构建(通过SMILES)。
