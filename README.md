# Simple_DPO
简单DPO算法实战
## 数据集
比如：回答的的从两个变为三个
问题：36=
rejected：15+21
chosen：10+12+14
## 训练过程
1. 是在构造数据集，通过对同一问题的两种回复的倾向性：`chosen` or `rejected`，反映人类偏好。
2. 在于优化，具体过程大概是，对于同一个`question prompt`，模型在两种模型：`policy model`(model_gen) 和 `reference model`(model_gen_ref)下分别生成，对应chosen 和 rejected label真值标签的生成概率，因此可以获得**四种概率值**：`policy_chosen_logps`, `policy_rejected_logps`, `reference_chosen_logps`, `reference_rejected_logps`, 用于DPO loss计算。
3. `prob_log_diff`即：policy_chosen_logps减去policy_rejected_logps。`prob_log_diff_ref`同理。最终的损失即prob_log_diff和prob_log_diff_ref之间的`KL散度`。(有问题不该只看kl散度)
![](./img/DPO%E8%AE%AD%E7%BB%83%E8%BF%87%E7%A8%8B.png)