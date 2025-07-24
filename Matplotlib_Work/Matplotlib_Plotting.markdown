# 关于使用Python的Matplotlib画图

## 基础尺寸控制

```py
plt.figure(figsize=(4, 3)) # 小尺寸
plt.figure(figsize=(10, 5))  # 宽屏尺寸
```

---

## DPI（每英寸点数）的影响 —— DPI 决定每英寸包含的像素数量

```py
plt.figure(figsize=(5, 5), dpi=80)  # 400×400 像素 (5*80=400)
plt.figure(figsize=(5, 5), dpi=150)  # 750×750 像素 (5*150=750)
```

---

## 实际应用场景

### 论文图表（单栏）

```py
plt.figure(figsize=(3.5, 2.5))  # 学术期刊常用尺寸
plt.tight_layout(pad=0.5)  # 紧凑布局
plt.savefig("paper_figure.png", dpi=300)  # 高DPI用于印刷
```

### 演示文稿幻灯片

```py
plt.figure(figsize=(10, 6))  # 16:9宽屏比例

```

### 网页/报告宽图

```py
plt.figure(figsize=(12, 4))  # 超宽图表（时间序列用的多）
```

---

## 尺寸控制技巧

### 黄金比例（美学最佳比例）

```py
golden_ratio = (1 + 5**0.5) / 2  # ≈1.618
height = 6
width = height * golden_ratio

plt.figure(figsize=(width, height))
```

### 与子图协同工作

```py
fig, axs = plt.subplots(2, 2, figsize=(10, 8))  # 2×2网格

axs[0, 0].set_title("左上")
axs[0, 1].set_title("右上")
axs[1, 0].set_title("左下")
axs[1, 1].set_title("右下")

plt.tight_layout()
```

---

## 常见问题解决方案

### 图表元素重叠或太拥挤

```py
plt.figure(figsize=(10, 8))  # 增加尺寸
plt.plot(...)
plt.tight_layout(pad=2.0)  # 增加内边距
```

### 保存的图像尺寸不对

```py
plt.figure(figsize=(8, 6))
# 保存时指定DPI控制像素尺寸
plt.savefig("output.png", dpi=150, bbox_inches="tight")
# 最终像素尺寸：8*150=1200px × 6*150=900px
```

---

# 总结

## 常用尺寸参考

- **论文图表：(3.5, 2.5) 或 (7, 5)**
- 演示文稿：(10, 6) (16:9) 或 (10, 7.5) (4:3)
- 网页嵌入：(8, 6) 或 (10, 5)

## DPI设置指南：

- 屏幕显示：72-150 DPI
- **学术出版：300-600 DPI**
- 海报打印：150-300 DPI

## 尺寸调整原则（根据内容复杂度调整尺寸）

- (6, 4)
- (10, 8)
- (12, 9)

## 专业技巧（使用GridSpec精确控制子图布局）

```py
from matplotlib.gridspec import GridSpec

fig = plt.figure(figsize=(12, 8))
gs = GridSpec(2, 2, width_ratios=[3, 1], height_ratios=[1, 3])

ax1 = fig.add_subplot(gs[0, 0])
ax2 = fig.add_subplot(gs[1, 0])
ax3 = fig.add_subplot(gs[:, 1])
```
