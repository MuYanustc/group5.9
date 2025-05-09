---
# You can also start simply with 'default'
theme: slidev-theme-ustc
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /bg.png
# some information about your slides (markdown enabled)
title: group5.9
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
hideInToc: true
---

# 古井贡酒摊晾降温



<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->
---
layout: two-cols

---

# 目录
<Transform scale = 1.2>
<Toc minDepth="1" maxDepth="1" />
</Transform>

---
layout: two-cols
transition: fade-out
---

<!-- # Left -->


# 基本情况

* 总体介绍：

一段链板，出料机从链板一端出料，链板上方有风机，风机可调速或开关。链板上有传感器，实时监测链板上的温度。目标是控制链板出端的温度在目标区间。

* 基本元素：
  * 一段定长链板
  * 三对定频风机
  * 三对变频风机


::right::
<!-- # Right -->

<br>
<br>

* 可变参数：
  * 链板速率
  * 出料速率
  * 风机转速/开关

* 环境参数：
  * 环境温度
  * 环境湿度

---
layout: image
image: /lct.png
backgroundSize: 98% 
transition: fade-out
---

# 流程图

一个车间两条摊晾产线
<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/features/slide-scope-style
-->
---
layout: image-left
transition: fade-in
image: /lb.png
---

# 现有问题

<br>
<Transform scale = 1.2>

* 自动控温装置仅在环境温度为15~20时开启，其他条件控制效果不佳
* 因为料有粘性，导致链板上方测温不准。

</Transform>
<br>
<br>

# 解决方案

<br>
<Transform scale = 1.2>

* 根据历史经验和物理模型，辅助控温
* 加装更准的测温仪器

</Transform>
<br>

<!--
Here is another comment.
-->

---
layout: two-cols
transition: slide-up
---

# 物理规律

### 热对流散热

牛顿降温定律假设：
> 物体温度变化速率，正比于它与环境温度的差值。

也就是说，  
物体的瞬时温度变化率 $\frac{dT}{dt}$ 与它当前温度 $T(t)$ 和环境温度 $T_{\text{env}}$ 的差值成正比。

数学表达式如下：
$\dfrac{dT}{dt} = -\frac{k}{m c}\bigl(T(t) - T_{\text{env}}\bigr)$

其中：

* $T(t)$：物体在时间 $t$ 时的温度
* $T_{\text{env}}$：环境温度（假设为常数）
* $k$：正比例系数（正值），表示降温速率
* $m$, $c$: 质量，比热容
::right::
<br>
<br>

###  蒸发散热

液体相变同样也会带走热量，摊晾过程中蒸发散热也是重要的一环。

* 蒸发带走热量：
  $Q_{\rm evap}=m_{\rm evap}L_v$
* 写成速率形式：
  $\frac{dT}{dt}=-\frac{L_v}{m c}m_{\rm evap}$

其中，$m_{\rm evap}$是一个衡量蒸发速率的参数，与**液体温度**，**环境湿度**有关，$L_v$是液体的汽化潜热。


将二者结合，得到：

$$
\frac{dT}{dt}
= -\,\underbrace{\frac{k}{m c}}_{k_{\rm conv}}\,(T - T_{\rm env})
\;-\;
\underbrace{\frac{\dot m_{\rm evap}\,L}{m c}}_{\displaystyle \;k_{\rm evap}}
$$

<!-- https://sli.dev/guide/animations.html#click-animation -->

---
layout: two-cols
transition: slide-up
---

# 基本想法


<v-click>
  <h2>
    what we have:
  </h2>
</v-click>

<br>
<br>

<v-clicks every = 2>

* $T_{start}$: 起始温度，暂时均以90℃代替
* $T_{end}$: 目标温度，设为18℃
* $T_{env}$: 环境温度
* $H_{env}$: 环境湿度
* $f_{fan}$: 风机转速/开关
* $v_{l}$: 链板速率，速率越大，摊晾时间越短
* $v_{m}$: 出料速率，速率越大，料越多 

</v-clicks>


::right::

<br>
<br>

<v-click>
  <h2>
    what we want:
  </h2>
</v-click>


<v-clicks>

* 根据历史数据和物理模型，拟合出公式中缺失的常数。也可以做适当的近似，降低模型的复杂度。
* 测试时，根据：
  * $T_{env}$: 环境温度
  * $H_{env}$: 环境湿度
    
  计算出相应的:
  * $f_{fan}$: 风机转速/开关
  * $v_{l}$: 链板速率
  * $v_{m}$: 出料速率
</v-clicks>

---
layout: two-cols
transition: slide-up
---

# 后续工作

<Transform scale = 2>

* 蒸发散热公式较多，选取较为合适的公式建模。
* 加入蒸发模型后模型未知参数变多，需要近似或者采取别的方法。
* 原有模型控温中大量采用了负反馈调节，需要分析一下可行性。

</Transform>
---
layout: center
class: 结束
hideInToc: true
---

# Thank you!