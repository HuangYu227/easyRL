# common
- 都在学动作价值函数
$$G_{t} = r_{t+1} + \gamma r_{t+2} + \gamma^{2} r_{t+3} + \dots$$
$$Q^{\pi}(s, a) = \mathbb{E}_{\pi}[G_t \mid s_t = s, a_t = a]$$
- 两种算法都是用于控制：想得到最优策略$π^*$以及对应的最优价值$Q^{*}(s, a) = \max_{\pi} Q^{\pi}(s, a)$

# difference
- SARSA$(s, a, r, s', a')$ 使用贝尔曼期望方程
$$ Q^{\pi}(s, a) = \mathbb{E} [r + \gamma \mathbb{E}_{a' \sim \pi(\cdot | s')} Q^{\pi}(s', a') | s, a] $$
- 用一次样本(s,a,r,s′,a′)近似期望：
$$\mathrm{target}_{\mathrm{SARSA}} = r + \gamma Q(s', a')$$

- 迭代
$$Q(s,a) \leftarrow Q(s,a)+α(r+γQ(s',a')-Q(s,a)) $$
---------------------------------------------------------------------
- 贝尔曼最优方程（最优策略）
$$Q^{*}(s, a) = \mathbb{E}[r + \gamma \max_{a'} Q^{*}(s', a') | s, a]$$
- 用一次样本 (s,a,r,s′) 近似期望：
$$\mathrm{target}_{\mathrm{Q-learning}} = r + \gamma \max_{a'} Q(s', a')$$
- 迭代
$$Q(s,a)\leftarrow Q(s,a)+α(r+γ\max_{a'}Q(s',a')-Q(s,a) ) $$
---------------------------------------------------------------------


![](../../../Pasted%20image%2020260227132219.png)









