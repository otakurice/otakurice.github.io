---
title: markdown学习笔记
date: 2018-08-23 09:21:01
tags:
- markdown
categories:
- 前端
---

### 一、 公式

#### 1. 显示于行内： $\color {blue} {f(x)=x} $

`$ f(x)=x $`

#### 2. 独立显示一行：

`$$ s=\sum_1^n{n_i} $$`
<font color=#0000ff>$$ s=\sum_1^n{n_i} $$</font>

#### 3. 角标

- **上标：**<font color=#0000ff>$ x^2 $</font>
`$ x^2 $`
- **下标：**<font color=#0000ff>$ x_i $</font>
`$ x_i $`
- **上下左右标：**<font color=#0000ff>$ \sideset{^1_2}{^3_4}\bigotimes $</font>
`$ \sideset{^1_2}{^3_4}\bigotimes $`

#### 4.下划线、上划线

- **上划线命令：** `\overline{公式}`
- **下划线命令：** `\underline{公式}`
<font color=#0000ff>$\overline{\overline{a^2}+\underline{ab}+\bar{a}^3}$</font> `$\overline{\overline{a^2}+\underline{ab}+\bar{a}^3}$`
- **上花括弧命令：** `\overbrace{公式}{说明}`
- **下花括弧命令：** `\underbrace{公式}_{说明}`
`$ \underbrace{a+\overbrace{b+\dots+b}^{m个}}_{20个} $`
<font color=#0000ff>$$ \underbrace{a+\overbrace{b+\dots+b}^{m个}}_{20个} $$</font>

#### 5. 括号：
- **小括号与方括号**:原始的就好

- **大括号:** <font color=#0000ff>$ \lbrace a+x \rbrace $</font>
`$ \lbrace a+x \rbrace $`

- **尖括号:**<font color=#0000ff>$ \langle x \rangle $</font>
`$ \langle x \rangle $`

- **上取整: **<font color=#0000ff>$ \lceil \frac{x}{2} \rceil $</font>
`$ \lceil \frac{x}{2} \rceil $`

- **下取整: **<font color=#0000ff>$ \lfloor x \rfloor $</font>
`$ \lfloor x \rfloor $`

- **注意：**原始括号不会缩放,如 `$$ \lbrace \sum_{i=0}^{n}i^{2}=\frac{2a}{x^2+1} \rbrace $$`
<font color=#0000ff>$$ \lbrace \sum_{i=0}^{n}i^{2}=\frac{2a}{x^2+1} \rbrace $$</font>
需要加入 \left \right   `$$ \left\lbrace \sum_{i=0}^{n}i^{2}=\frac{2a}{x^2+1} \right\rbrace $$`
<font color=#0000ff>$$  \left\lbrace \sum_{i=0}^{n}i^{2}=\frac{2a}{x^2+1} \right\rbrace $$</font>

#### 6.求和与积分：

- **\sum 求和**，`$$ \sum_i^n $$`下标表示求和下限，上标表示求和上限
<font color=#0000ff>$$ \sum_i^n $$</font>

- **\int 积分**，`$\$ \int_{1}^{\infty} $$`下标表示积分下限，上标表示积分上限
<font color=#0000ff>$$ \int_{1}^{\infty} $$</font>

- **\prod 求积**，`$$ \prod_{1}^{n} $$`
<font color=#0000ff>$$ \prod_{1}^{n} $$</font>

- **\bigcup 求并集**，`$$ \bigcup_{1}^{n} $$`
<font color=#0000ff>$$ \bigcup_{1}^{n} $$</font>

- **\iint 双重积分**，`$$ \iint_{1}^{n} $$`
<font color=#0000ff>$$ \iint_{1}^{n} $$</font>

- **改变上下限位置的命令：** \limits(强制上下限在上下侧) 和 \nolimits(强制上下限在左右侧)
<font color=#0000ff>$\sum\limits_{k=1}^n$</font> `$\sum\limits_{k=1}^n$`
<font color=#0000ff>$\sum\nolimits_{k=1}^n$</font> `$\sum\nolimits_{k=1}^n$`

#### 7.分式与根式
- **分式：**`$$ \frac ab $$`
<font color=#0000ff>$$ \frac ab $$</font>
`$$ \frac{1}{2} $$`
<font color=#0000ff>$$ \frac{1}{2} $$</font>
`$$ {a+1 \over b+1} $$`
<font color=#0000ff>$$ {a+1 \over b+1} $$</font>
**连分式：** `$$ x_0+\frac{1}{x_1+\frac{1}{x_2+\frac{1}{x_3+\frac{1}{x_4}}}} $$`
<font color=#0000ff>$$ x_0+\frac{1}{x_1+\frac{1}{x_2+\frac{1}{x_3+\frac{1}{x_4}}}}$$</font>

- **根式：**`$$ \sqrt[x+1]{x^2} $$`
<font color=#0000ff>$$ \sqrt[x+1]{x^2} $$</font>
被开方表达式字符高度不一致时，根号上面的横线可能不是在同一条直线上；为了使横线在同一条直线上，可以在被开方表达式插入一个只有高度没有宽度的数学支柱\mathstut
<font color=#0000ff>$\sqrt{a}+\sqrt{b}+\sqrt{c}$</font> `$\sqrt{a}+\sqrt{b}+\sqrt{c}`
<font color=#0000ff>$\sqrt{\mathstrut a}+\sqrt{\mathstrut b}+\sqrt{\mathstrut c}$</font> `$\sqrt{\mathstrut a}+\sqrt{\mathstrut b}+\sqrt{\mathstrut c}$`

#### 8. 集合

- **大括号：**
<font color=#0000ff>$\{...\}$</font> `$\{ ...\}$`
- **属于：**
<font color=#0000ff>$ \in $</font> `$\in$`
- **不属于：**
<font color=#0000ff>$\not\in$</font> `$\not\in$`
- **A包含于B：**
<font color=#0000ff>$A\subset B$</font> `$A\subset B$`
- **A真包含于B：**
<font color=#0000ff>$A \subsetneqq B$</font> `$A \subsetneqq B$`
- **A包含B：**
<font color=#0000ff>$A \supset B$</font> `$A \supset B$`
- **A真包含B：**
<font color=#0000ff>$A \supsetneqq B$</font> `$A \supsetneqq B$`
- **不包含于：**
<font color=#0000ff>$A \not \subset B$</font> `$A \not \subset B$`
- **交集：**
<font color=#0000ff>$A \cap B$</font> `$A \cap B$`
- **并集：**
<font color=#0000ff>$A \cup B$</font> `$A \cup B$`
- **闭包：**
<font color=#0000ff>$\overline{A}$</font> `$\overline{A}$`
- **A减去B：**
<font color=#0000ff>$A\setminus B$</font> `$A\setminus B$`
- **实数集合：**
<font color=#0000ff>$\mathbb{R}$</font> `$\mathbb{R}$`
- **空集：**
<font color=#0000ff>$\emptyset$</font> `$\emptyset$`



#### 9.运算符

- **乘：**
<font color=#0000ff>$ x \times y $</font>`$ x \times y $`
<font color=#0000ff>$ x \cdot y $</font>`$ x \cdot y $`
<font color=#0000ff>$ x \ast y $</font>`$ x \ast y $`

- **除：**
<font color=#0000ff>$ x \div y $</font>`$ x \div y $`

- **加减：**
<font color=#0000ff>$ x \pm y $</font>`$ x \pm y $`

- **减加：**
<font color=#0000ff>$ x \mp y $</font>`$ x \mp y $`

- **小于等于：**
<font color=#0000ff>$ x \leq y $</font>`$ x \leq y $`

- **大于等于：**
<font color=#0000ff>$ x \geq y $</font>`$ x \geq y $`

- **不大于等于：**
<font color=#0000ff>$ x \ngeq y $</font>`$ x \ngeq y $`

- **不大于等于：**
<font color=#0000ff>$ x \not\geq y $</font>`$ x \not\geq y $`

- **不等于：**
<font color=#0000ff>$ x \neq y $</font>`$ x \neq y $`

- **约等于：**
<font color=#0000ff>$ x \approx y $</font>`$ x \approx y $`

- **恒等于：**
<font color=#0000ff>$ x \equiv y $</font>`$ x \equiv y $`

- **定义运算符：**
<font color=#0000ff>$ x \bigodot y=x+y^2 $</font>`$ x \bigodot y=x+y^2 $`

- **定义运算符：**
<font color=#0000ff>$ x \bigotimes y=x+y^2 $</font>`$ x \bigotimes y=x+y^2 $`

#### 10.带帽符号

- <font color=#0000ff>$ \hat{xy} $</font> `$ \hat{xy} $ `
- <font color=#0000ff>$ \widehat{xyz} $</font> `$ \widehat{xyz} $`
- <font color=#0000ff>$ \tilde{xy} $</font> `$ \tilde{xy} $`
- <font color=#0000ff>$ \widetilde{xyz} $</font> `$ \widetilde{xyz} $`
- <font color=#0000ff>$ \check{x} $</font> `$ \check{x} $`
- <font color=#0000ff>$ \breve{y} $</font> `$ \breve{y} $`
- <font color=#0000ff>$ \grave{x} $</font> `$ \grave{x} $`
- <font color=#0000ff>$ \acute{y} $</font> `$ \acute{y} $`



### 二、字体
- **黑板粗体字：**
<font color=#0000ff>$ \Bbb SAMPLE$</font>`$ \Bbb 字母$`

- **字号：**
<font color=#0000ff>$\tiny 萌萌哒$</font>`$\tiny 萌萌哒$`
<font color=#0000ff>$\scriptsize 萌萌哒$</font>`$\scriptsize 萌萌哒$`
<font color=#0000ff>$\small 萌萌哒$</font>`$\small 萌萌哒$`
<font color=#0000ff>$\normalsize 萌萌哒(正常)$</font>`$\normalsize 萌萌哒(正常)$`
<font color=#0000ff>$\large 萌萌哒$</font>`$\large 萌萌哒$`
<font color=#0000ff>$\Large 萌萌哒$</font>`$\Large 萌萌哒$`
<font color=#0000ff>$\huge 萌萌哒$</font>`$\huge 萌萌哒$`
<font color=#0000ff>$\Huge 萌萌哒$</font>`$\Huge 萌萌哒$`

- **占位宽度：**
<font color=#0000ff>$ a \qquad b $</font>`$ a \qquad b $` 两个m的宽度
<font color=#0000ff>$ a \quad b $</font>`$ a \quad b $` 一个m的宽度
<font color=#0000ff>$ a\ b $</font>`$ a\ b $` 1/3m宽度
<font color=#0000ff>$ a\;b $</font>`$ a\;b $` 2/7m宽度
<font color=#0000ff>$ a\,b $</font>`$ a\,b $` 1/6m宽度
<font color=#0000ff>$ ab $</font>`$ ab $` 没有空格
<font color=#0000ff>$ a\!b $</font>`$ a\!b $` 紧贴，缩进1/6m宽度

参考资料：
https://www.zybuluo.com/codeep/note/163962#cmd-markdown-%E5%85%AC%E5%BC%8F%E6%8C%87%E5%AF%BC%E6%89%8B%E5%86%8C
https://blog.csdn.net/yzr1183739890/article/details/64130912
https://blog.csdn.net/garfielder007/article/details/51646604
