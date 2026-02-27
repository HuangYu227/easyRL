需要模型：转移概率 P(s′∣s,a)、奖励 R(s,a)、折扣 γ，有策略
# policy iteration
- 分成策略评估、策略提升
- 输入状态集合 S、动作集合 A、P,R,γ、策略π
- 输出最有价值函数
#### 策略评估
在给定策略下求贝尔曼期望方程，通过迭代方式求解，解析解效率低
将每一个状态$s_t$不断自举得到稳定值
$$V^{\pi}(s) = \sum_{a} \pi(a|s) \sum_{s'} P(s'|s, a) (R(s, a, s') + \gamma V^{\pi}(s'))$$
$$P(s' \mid s,a)*\pi(a \mid s)=P(s' \mid s)$$
$$V = R+γPV$$
#### 策略改进
Q是依赖V的
$$π_{i+1}(s)=argmax_a (Q_{πi}(s,a)) $$
$$Q_{πi}(s,a) = R(s,a)+γ\sum_{s'∈S}p(s' \mid s,a)V_{πi}(s') $$


# value iteration
求解最优价值函数以及最优策略
同样需要P，R。无策略
贝尔曼最优备份
$$Q_{k+1}(s, a) = R(s, a) + \gamma \sum_{s' \in \mathcal{S}} p(s' | s, a) V_{k}(s')$$
$$V_{k+1}(s) = \max_{a} Q_{k+1}(s, a)$$
$$\pi(s) = \arg \max_{a} \left[ R(s, a) + \gamma \sum_{s' \in \mathcal{S}} p(s' | s, a) V_{H+1}(s') \right]$$





