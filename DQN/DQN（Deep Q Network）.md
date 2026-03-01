**Q-learning缺点**
- 当状态或者动作连续的时候，就有无限个状态动作对，我们更加无法使用这种表格形式来记录Q各个状态动作对的值。

用DQN
DQN有几个问题需要解决
- 捕捉的连续画面的帧具有时序相关性，这在训练中会造成干扰
- 无法利用已经用过的帧
- Q值的微小更新会显著影响策略
- $Q \leftarrow Q + \alpha(r+\gamma Q(s',a)-Q)$出现的target和Q存在相同的网络参数
**solution**
- 设置经验存放内存区
	- 容量为N，（s,a,r,s'），每次将环境中得到的四元组存进去
	- 随机抽样消除了马尔科夫相关性（序列相关性），能更有效利用过去经验
	- 避免灾难性遗忘
- 目标网络
	- 目标值会动，把目标网络固定住，让训练网络逼近估计值
	- 每隔C步从Q网络复制参数来更新目标Q网络
	- 这样可以切断两个网络相关性
**pipeline**
- ![[Pasted image 20260301174457.png]]
- 论文中Q'的更新是硬更新直接赋值，代码实践中用的软更新，采用残差连接的思想，用$\tau$加权平均，
- $$\mathrm{args}.\tau * \mathrm{q\_network\_param}.\mathrm{data} + (1.0 - \mathrm{args}.\tau) * \mathrm{target\_network\_param}.\mathrm{data}$$




深度Q网络 是基于价值的算法，在基于价值的算法里面，我们学习的不是策略，而是**评论员（critic）**。

- 基于蒙特卡洛的方式方差相较于某一个状态的奖励更大，有
$$Var[kX]=k^2Var[X] $$
- 基于时序的方法我们想最小化
- 这种方式r也是随机变量，但是相比较于G的所有状态都有r比方差更小，考虑$V_{\pi}$的估计不一定准确，所以学习出来的结果也不准确
- $$V_{\pi}(s_{t}) \longleftarrow r + V_{\pi}(s_{t+1})$$













![[Pasted image 20260228142802.png]]
- 既然不能用表，那我们就用一个函数去拟合
- 用一个“能输入 s,a 输出一个数”的模型，去逼近真正的 Q 函数。
$$Q(s,a)≈Q_w(s,a) $$
	$w$是模型参数
	所以现在的问题是用什么去拟合复杂情况，神经网络就是因为表达能力强所以拟合效果好
	神经网络表示 $Q_w(s,a)$，我们把它叫 **Q 网络（Q-network）**
	状态数无穷多我们用函数拟合，这可以处理动作数无限和有限的情况，通常 DQN（以及 Q-learning）只能处理动作离散的情况，因为在函数$Q$的更新有$max_a$操作![[Pasted image 20260228144256.png]]
	![[Pasted image 20260228144317.png]]
	$$Q(s, a) \leftarrow Q(s, a) + \alpha \left[r + \gamma \max_{a' \in \mathcal{A}} Q(s', a') - Q(s, a) \right]$$
	构造下面的损失函数：
	$$\omega^{*} = \arg \min_{\omega} \frac{1}{2N} \sum_{i=1}^{N} \Big[ Q_{\omega}(s_{i}, a_{i}) - (r_{i} + \gamma \max_{a'} Q_{\omega}(s_{i}', a')) \Big]^{2}$$
	乘以2的原因是求梯度的时候可以约分，N则是用来平均误差，让损失更稳定
	至此，我们就可以将 Q-learning 扩展到神经网络形式——**深度 Q 网络**（deep Q network，DQN）算法。


#### 经验回放
![[Pasted image 20260228153450.png]]

#### 目标网络
- $\gamma \max_{a'} Q_{\omega}(s_{i}', a'))$是目标，目标也在变，会导致训练不稳定
- 想法是将TD目标的Q网络固定住：
- ![[Pasted image 20260228154502.png]]
$$\omega \leftarrow \omega - \alpha \nabla_{\omega} L(\omega)$$
只要你训练了一步，$\omega$就会改变——因为你在把网络输出 $\omega(s,a)$ 往目标 y上拟合。

![[Pasted image 20260228155213.png]]













