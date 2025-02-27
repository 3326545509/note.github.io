# FreeFEM教程
[官网](https://doc.freefem.org/introduction/index.html) 同时也提供了pdf下载地址

这款有限元方法的软件的优点:
* 普适化: 目标仅仅是求解偏微分方程, 所以不是为了特定的需求(比如算P-SV)设计的
* 优雅: 它省略了繁复的代码, 但是保留了有限元方法最基本的框架, 让用户能够自由更改以适应不同的问题, 但是又没有用无聊的细节来打扰用户
* 逻辑清晰: 它的代码构建过程完整再现了FEM方法的基本大步骤, 可以说写它的代码就相当于写”FME方法的伪代码”, 只要对FEM方法对理论有了解就能驾驭软件

让我想起了类似的软件comsol, 但是它的图形化界面让构建复杂模型和求解特殊偏微分方程变得很麻烦, 它本质上是一个适用若干已设定好的问题的软件. 

一位专家的[教学ppt](http://ionut.danaila.perso.math.cnrs.fr/zdownload/FFEM/), 有很多值得借鉴和学习的[案例](http://ionut.danaila.perso.math.cnrs.fr/zdownload/Tutorial_2019_Singapore/), 涉及边界设置,方程设置等


## 一个完整的FEM代码需要完成的步骤
* 设置边界
* mesh
* 填充有限元(选取基函数)
* 设置初始条件
* 设置待求解方程
  * 方程的弱化
  * 加上边界条件(这一步可以省略,用默认的边界条件)
* 求解方程(如果像波动方程那样含有时间,则需要写一个循环进行迭代)
* 输出结果

## 案例
软件用的代码基础是C++, 诸如 int age = 25; 可以看到很多类似的结构. “类型”,“变量名”和“值”别搞错了

运行方法: FreeFem++ example.edp

求解波动方程:
$$
u_{tt}+\alpha u_t - c^2 \Delta u=f
$$

具体离散化、方程弱化: 略.
```
// 声明必要变量,用来划分网格区域
real xc1=-80, yc1=-200;
real x0 = -80;
real x1 = 320;
real y0 = -200;
real y1 = 200;
int n = 50;

// 声明变量
//注意u, v在这里声明. 默认u是待求场(eg波场, 温度场), v是test function
real fm=0.06, c=3;
real tmax=110, tmin=-20, dt=0.1, idt2 = 1./(dt*dt), t, error=1e-10; int iter=0, nplot=2;
real[int] output1((tmax-tmin)/dt+2);

// 划分网格
mesh Th = square(n, n, [x0+(x1-x0)*x, y0+(y1-y0)*y]);
// 给网格填充基函数
fespace Vh(Th,P2b);
// 自定义函数. macro和//EOM组合起来用, 两个都不能省略
macro grad(u) [dx(u),dy(u)]//EOM
// 声明波场,带上Vh标识就表示是全域的一个函数, 而不是单个值, eg可以调用u(10,12)表示x=10km, y=12km的u的值
Vh u=0,v,uold=0,uvold=0;
// 设置默认输出的信息多少, 0表示没有, 1表示一些, 2表示详细信息
verbosity=0;

t = tmin;
// 由于波动方程是含有时间的, 所以需要迭代
for (iter=0; t<=tmax; ++iter){
    // 定义函数 func 注意和macro不一样
    func f= 1/pi*error/(x^2+y^2+error^2)*(-1)*(1-2*pi^2*fm^2*t^2)*exp(-pi^2*fm^2*t^2)*1e10;
    
    // 定义方程, 这里是弱化后的方程, (理论知识可以来咨询本人, 不作赘述)
    problem WaveEquation(u,v) =  int2d(Th)(idt2*u*v)
                                - int2d(Th)(2*idt2*uold*v)
                                + int2d(Th)(idt2*uvold*v)
                                + int2d(Th)(c^2*grad(uold)'*grad(v))
                                - int2d(Th)(f*v)
                                ;
    // 调用刚刚定义的problem求解方程
    WaveEquation;
    
    //保留波场和画图
    output1[iter]=u(240,0); //把x=240, y=0的波场保留, 注意240不是index, 而是比如km, m这样的物理量.
    if (!(iter%100)){
        plot(u,fill=true,grey=true,dim=3,wait=false);
        cout<<iter<<endl;
    }
    
    // 迭代中更新波场
    uvold = uold;
    uold = u;
    t+=dt;

    
}

//输出文件
ofstream f1out("array1.txt");
for (int i=0;i<((tmax-tmin)/dt);++i){
    f1out<<output1[i]<<endl;
}

plot(u,fill=true,grey=true,dim=3,wait=true);
```
## 保留字符
* **u**
  * 待求场, 即偏微分方程里的未知数
* **v**
  * test function, 用来弱化方程 一般情况下用默认的就好,不需要进行任何设置
* **x, y, z**
  * 3个空间坐标
* **int2d**
  * 用法: int2d(积分区域)(被积函数)
  * 例子: int2d(Th)(dx(u)*dx(u)) 注意Th是网格区域, 而不是填充有限元之后的区域
* **solve**
  * solve Name (u,v) = int2d( )( ) + int2d( )( ) + on(C,u=0)
  * 定义待求解方程, 通过on加边界条件
* **border**
  * border Boundary1(t=0,pi){x=cos(t);y=sin(t);}
  * 可以用参数方程来定义边界
* **mesh**
  * mesh Th = buildmesh( C0(50)+C1(10)+... )
  * 括号里面是用来mesh的边界, 每一条边界上用多少个网格通过括号里的数字决定. 
  * 注意如果是一个方形区域,边界的顺序必须从左下角那个点逆时针转一圈, 定义C0的border参数方程也要遵循这一原则
  * 边界必须“密闭”, 否则无法进行网格划分
* **fespace**
  * fespace Vh(Th,P1)
  * 给网格区域填基函数
* **func**
  * func f=x*y
  * 定义函数, 在其他地方可以直接用f
* **dy(u)**
  * 表示partia u/partial y
  * dy(u)(3,4)表示在x=3, y=4位置上的partia u/partial y
* **region**
  * 具体在官网transmission problem一栏可以看到
  * pdf p62第37行的使用形式比官网的更自然易懂
* **verbosity**
  * 显示模拟过程中程序默认输出到屏幕的中间信息的数量, verbosity=0表示输出极少
  * 用户手动设置的由cout输出的信息不受到这个函数的影响

## 习惯字符
* **Th**
  * 网格化之后的区域.
  * {Tk}k=1...nt 
  * h是网格数量, nt是三角形的数量, nv是rectrices的数量, 这些一般不会在代码里出现. 
* **Vh**
  * 填充了基函数之后的空间
* **Γ**
  * 通常指边界
  * Γj通常指一段一段的边界

## 特殊用法
* uold[ ]=u[ ]
* u(2,3)表示返回x=2,y=3位置的值
* A‘*B表示矢量相乘
* [dx(u), dy(u)]表示定义了一个矢量

### 迭代mesh, 通过最粗糙的逐渐画复杂
```
// 更好的mesh
mesh Th = square(10, 10,[x0+(x1-x0)*x, y0+(y1-y0)*y]);  //the initial mesh
Th = adaptmesh(Th, 1./30., IsMetric=1, nbvx=10000);     //updated mesh
```
### 定义狄拉克函数
```
func f= 1/pi*error/(x^2+y^2+error^2) * sourceTimeFunction;    //狄拉克定义1
func f = (x^2 + y^2 <= 65 ) ? sourceTimeFunction : 0;         //狄拉克定义2
u(0,0)  =   -1*(1-2*pi^2*fm^2*t^2)*exp(-pi^2*fm^2*t^2);       //错误示范
```

用公式
$$
\delta(x)=\frac{1}{\pi}\frac{\epsilon}{x^2+\epsilon^2}
$$

$$
\delta(x)=\frac{1}{dx}
$$
在FEM里不能直接在某一个点上赋值