# ch1线性规划

---

> 公式示例

$$
\begin{equation}
	x = \begin{cases}
	1, &x>2 \\
	2, &x>3 \\
	\end{cases}
\end{equation}
$$

> Matlab中，线性规划的标准型为：
>
> 下标的正下方写法： \mathop{ \变量，在这里加斜杠是改为 非斜体 }_{ 正下方的下标 }
>
> 空格：\quad
>
> 
>
> 大于等于号：\geq
> 后面记得加空格，不然识别出错。
>
>  
>
> 小于等于号：\leq
>

### Matlab中，线性规划的标准型

$$
\begin{equation}
	\mathop{\min}_{x} \quad c^Tx \\
	\begin{cases}
		Ax \leq b \\
		Aeq·x = beq \\
		lb \leq x \leq ub\\
	\end{cases}
	
\end{equation}
$$

```matlab
% 注：c的转置(T) 是一个行向量，则 输入linprog中的c是列向量！！即：如下这样写！！
% c = [ 2;
% 		3;
%       4;
%      ]
% 其余的都按标准型来写即可
[ x,fval ] = linprog( c,A,b,
					  Aeq,beq,
                      lb,ub,
                      x0, OPTIONS ); % 参数的前三行，都是按照标准型方程书写下来的；
                      				 % x0是初始值，OPTIONS是控制参数。                  
```



### 可转化为线性规划的问题

$$
min\quad|x_1|+|x_2|+|x_3|+……+|x_n| \\
s.t. \quad\quad Ax\leq b
$$

​	注意到事实：对任意的 $$x_i$$，存在 $$u_i（u_i可以为0啊！）,vi>0$$，满足:
$$
x_i = u_i - v_i ,\quad |x_i| = u_i + v_i
$$
详情见 ch1 线性规划PDF。