# 不定积分过程生成器（ByMathematica）

## 安装Rubi库(Install Rubi)

如果 Mathematica 版本![1](http://latex.codecogs.com/svg.latex?\geqslant11.3)

可直接运行

```mathematica
ResourceFunction["GitHubInstall"]["RuleBasedIntegration","Rubi"]
```

版本低的就下载这个 <https://github.com/RuleBasedIntegration/Rubi/releases/download/4.16.1.0/Rubi-4.16.1.0.paclet>

然后运行

```mathematica
PacletInstall["PATHto.paclet"]
```

## 然后，运行下面的代码(Run following codes)

```mathematica
<<Rubi`
IntWithStepsOfTeXForm[expr_,var_]:=With[{TeX2Str=Convert`TeX`ExpressionToTeX},
Steps[Int[expr,var],RubiPrintInformation->False]//
Flatten//
Most//
Cases[RubiIntermediateResult[x_]:>"=&"<>(TeX2Str[HoldForm@@x])<>"\\\\"]//
{"\\begin{aligned}",TeX2Str@HoldForm@Int[expr,var],##&@@#,"\\end{aligned}"}&//
StringReplace[{"\\,d"->"\\,\\mathrm{d}"}]//
StringRiffle]
```

### 下面是一些解题展示

```mathematica
IntWithStepsOfTeXForm[Sin[x]/x^3,x]
```

$$\begin{aligned}\int\frac{\sin(x)}{x^3}\mathrm{d}x=&-\frac{\sin(x)}{2x^2}+\frac{1}{2}\int\frac{\cos(x)}{x^2}\mathrm{d}x\\\\=&-\frac{\cos(x)}{2x}-\frac{\sin(x)}{2x^2}-\frac{1}{2}\int\frac{\sin(x)}{x}\mathrm{d}x\\\\=&-\frac{\cos(x)}{2x}-\frac{\sin(x)}{2x^2}-\frac{\text{Si}(x)}{2}+C\end{aligned}$$

```mathematica
IntWithStepsOfTeXForm[(x^2+x+1)/(x^4+x^3+x+1),x]
```

$$\begin{aligned}\displaystyle\int\frac{1+x+x^2}{1+x+x^3+x^4}\,\mathrm{d}x=&\displaystyle\int\left(\frac{1}{3(1+x)^2}+\frac{2}{3\left(1-x+x^2\right)}\right)\,\mathrm{d}x\\\\=&-\frac{1}{3(1+x)}+\frac{2}{3}\displaystyle\int\frac{1}{1-x+x^2}\,\mathrm{d}x\\\\=&-\frac{1}{3(1+x)}-\frac{4}{3}\text{Subst}\left(\displaystyle\int\frac{1}{-3-x^2}\,\mathrm{d}x,x,-1+2x\right)\\\\=&-\frac{1}{3(1+x)}-\frac{4\tan^{-1}\left(\frac{1-2x}{\sqrt{3}}\right)}{3\sqrt{3}}+C\end{aligned}$$

本文目前发在了

- [知乎](https://zhuanlan.zhihu.com/p/139362547)

- [MSE](https://mathematica.stackexchange.com/questions/221487/how-to-directly-get-the-texform-of-each-steps-from-rubi/221488#221488)

- [超理](https://chaoli.club/index.php/5300/p1#p53320)

>Mathematica使用人数好少啊。。。
