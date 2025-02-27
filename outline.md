# Physics, mathematics, and understanding of seismology

25.02.12

各种[笔记](https://github.com/3326545509/note.github.io). pdf、html、markdown格式.
 


## 目录
* **T-matrix**
  * 一种基于高阶散射理论正演和反演波场的方法.
* **Hese_Matrix**
  * 海森矩阵, 一种和Jacobian矩阵有联系的, 用于反演问题的偏微分表达
* **Derivative**
  * 声波方程的一阶弗雷谢导数, 一阶和高阶波恩近似
* **Tromp2005**
  *  经典的全波形反演文章
*  **Frechet**
   *  Frechet导数, 全波形的 delta Chi 的导出, jacobian Matrix 的定义和运用.
   *  Frechet是一个更宽泛的概念, Jacobian是其中的一种情况
*  **Gateau_derivative**
   *  和Frechet类似的另一个倒数, 但是没有Frechet运用广.
* **FFT**
  * 理论和离散fft的区别, 相位振幅和实部虚部的关系, 能只取实部的原因.
* **FFT振幅相位**
  * 理论*连续非周期傅立叶变换*的两种形式, 一种是文献里最常使用的公式. 它与振幅和相位谱的关系
* **FFT_sin_cos**
  *  sin和cos函数的傅立叶变换,其中用到了狄拉克函数的定义
* **Dirac**
  *  狄拉克函数的三种定义及证明
* **Tensor**
  * 张量的理解和计算, 并矢的理解. 摘自Tromp地震学书的附录1
* **复变积分**
  * 柯西定理,柯西公式,洛朗展开,留数定理,大小圆弧约旦引理,实数积分转成复数域积分.
  * 这只是一个提纲式的摘抄. 具体细节需翻看邵陆兵讲义.
* **Laplace转极坐标**
  * 2D和3D的Laplace算符直角坐标转极坐标,二者有1/r和2/r的系数区别
* **1D_damping波动方程**
  * 一维带阻尼的波动方程, 有指数衰减项.
* **球谐函数**
  * 和邵路兵书中介绍的球谐函数思路有差异.分离变数,球谐函数,勒让德函数
  * 公式编号对应书Fourier acoustics sound radiation and farfield acoustical holography. Earl G Williams.
* **Green**
  * 波动方程的格林函数. 1D,2D和3D的. 通过频率波数域求解,变换回时间空间域.摘自[Purdue University](https://web.ics.purdue.edu/~nowack/geos557/lecture11-dir/lecture11.htm)
  * 可以帮助理解,但是没有实践意义. 实现反傅立叶变换的步骤才是求解这种方法的核心难点.
* **Green2D时频**
  * 2D波动方程的格林函数的时频傅立叶变换. 用到了贝塞尔函数的定义. 时间域的解(即第一个公式)摘自[Purdue University](https://web.ics.purdue.edu/~nowack/geos557/lecture11-dir/lecture11.htm)
* **Green3D2D波数求导**
  * 上文提到了格林函数在频率域求解.这里重点介绍了3D和2D的空间域位移如何转到频率域求导.这并不是一个想当然的过程. 1D的比较显然,同理可得,不细说.
* **Green2DStepFunc**
  * 2D波动方程的格林函数是一个阶跃函数和1/x形式函数的组合, 不是3D的狄拉克函数. 没有那么好的对称性, 性质更加复杂.
* **波动方程**
  * 零碎的波动方程的知识.摘自维基词条wave equation
* **FreeFEM**
  * 一种好用的开源FEM软件.