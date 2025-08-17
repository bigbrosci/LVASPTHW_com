# Ex3.6 VASP的输出文件 PROCAR

在 VASP 的静态（非分子动力学）计算中，**PROCAR 文件记录了每条能带的轨道投影波函数特征，包括 spd 轨道及对应离子的投影贡献**。投影值源于将 Kohn–Sham 波函数在每个离子附近的球内进行积分，得到各轨道类型的“贡献”值；**球外（密度泛函间区域）的贡献不包括在内**。这些投影数据可以帮助分析电子态的局域化性质和轨道贡献，常用于能带结构分析、轨道成分分析和胖带图（fat band）绘制等。更多的信息参考 VASP 官方 Wiki：[https://www.vasp.at/wiki/index.php/PROCAR](https://www.vasp.at/wiki/index.php/PROCAR)

---

## 1. 控制参数：
- **LORBIT < 10** 时，必须在 INCAR 文件中设置 `RWIGS`，用于定义每个离子投影区域的球半径。这时，轨道投影是基于**球谐函数**，区域仅限于由 `RWIGS` 确定的球体内。
- **LORBIT ≥ 10** 时，无需设置 `RWIGS`，投影是基于 VASP 所用的**投影算符（projector functions）**。

因此，根据计算需要选择合适的 LORBIT 值（11 或 12 常用）及是否设置 RWIGS。此外，当ISPIN = 2，以及 `LNONCOLLINEAR =.TRUE.` 时，PROCAR的信息会相应的变化。 

---

## 3. PROCAR 文件结构示例（LORBIT = 11）

```
# of k-points:    Nk    # of bands:   Nb    # of ions:   Ni

k-point     ik :   kx ky kz   weight = w

band     ib # energy  E # occ.  occ_value

ion      s     py    pz    px    dxy   dyz   dz2   dxz   x2-y2   tot
   1     ...   ...   ...   ...   ...   ...   ...   ...    ...    ...
   2     ...   ...   ...   ...   ...   ...   ...   ...    ...    ...
   ...
tot     ...   ...   ...   ...   ...   ...   ...   ...    ...    ...
```

- 第一行显示了网格总 k 点数、能带数量和离子总数；
- 接着每个 k 点的坐标和权重（weight）；
- 每个能带对应一段，包含能量值（energy）和占据数（occ）；
- 后面是每个离子按轨道（s、py、pz、px、dxy、dyz、dz2、dxz、x²−y²）投影后的贡献值，以及 tot 表示该离子的总贡献。

---

- 5. 并行设置注意事项

某些并行设置（例如 `NPAR ≠ 1`）可能导致 PROCAR 文件缺失或投影信息未输出。请确保并行参数不会影响 PROCAR 的生成。

此外，为正常获取 PROCAR，还需确保 `LORBIT` 与 `RWIGS` 设置正确。

---

## 6. 常见用途

- **绘制胖带图（Fat Band）**  
  将 PROCAR 中每条能带上各轨道的投影作为带图宽度，可以直观显示各轨道贡献。

- **轨道分析**  
  比如分析能带带性质（s、p、d 轨道成分），或对吸附态进行轨道贡献分解。

- **结合 PyProcar 可视化**  
  [PyProcar ](https://romerogroup.github.io/pyprocar5.6.6/#) 是一个 Python 工具，用于从 PROCAR 文件提取信息并绘图，支持能带可视化、DOS 投影等功能。

---

## 7. 简单小结

| 内容分类 | 要点 |
|----------|------|
| 控制参数 | LORBIT 决定投影方式；RWIGS 仅对 LORBIT < 10 有效 |
| 文件结构 | 每个 k 点、能带、离子均有对应投影值 |
| 投影意义 | 仅包含 RWIGS 球体内的成分，真实物理解释需结合态密度 DOS |
| 应用场景 | 胖带图、轨道成分、可视化工具（如 PyProcar） |
