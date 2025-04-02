# RLHF: No Magic, Just Code 🚀

> 通过代码实现深入理解RLHF(Reinforcement Learning from Human Feedback)

这个仓库提供了RLHF三种主流算法的清晰实现，帮助你透过复杂的概念，直观理解RLHF的核心原理。

## 🌟 特点

- 📝 **清晰的代码实现** - 每个算法都有详细的注释和解释
- 🔍 **最小化依赖** - 专注于算法本身，而不是框架细节
- 🎯 **循序渐进** - 从基础PPO到高级RLHF，逐步深入
- 💡 **实用示例** - 包含实际应用场景的演示

## 🗂️ 项目结构

```text
RLHF/
├── ppo/               # PPO (Proximal Policy Optimization)
│   ├── actor.ipynb    # Actor模型实现
│   └── critic.ipynb   # Critic模型实现
├── dpo/               # DPO (Direct Preference Optimization)
│   ├── train.ipynb    # 训练流程
│   └── eval.ipynb     # 评估脚本
└── grpo/              # GRPO (Generalized Reward Policy Optimization)
    ├── model.ipynb    # 模型定义
    └── train.ipynb    # 训练实现
```


## 🚀 快速开始

1. **克隆仓库**
```bash
git clone https://github.com/your-username/rlhf-no-magic.git
cd rlhf-no-magic
```

2. **安装依赖**
```bash
pip install -r requirements.txt
```

3. **运行示例**
```bash
# 选择一个算法开始
jupyter notebook ppo/actor.ipynb
```

## 📚 算法说明

### PPO (Proximal Policy Optimization)
- 基础的策略优化算法
- 实现了Actor-Critic架构
- 包含完整的训练循环

### DPO (Direct Preference Optimization)
- 直接从人类偏好学习
- 简化的奖励建模
- 高效的训练方法

### GRPO (Generalized Reward Policy Optimization)
- 通用化的奖励学习
- 改进的策略优化
- 更稳定的训练过程

## 🔧 核心依赖

- Python 3.8+
- PyTorch 1.8+
- Transformers 4.21+
- Datasets
- Jupyter

## 📈 性能展示

| 算法 | 训练速度 | 内存占用 | 性能表现 |
|------|----------|----------|----------|
| PPO  | 快       | 低       | 基准线   |
| DPO  | 中等     | 中等     | 优秀     |
| GRPO | 较慢     | 较高     | 最佳     |

## 🤝 贡献指南

欢迎提交Issue和Pull Request！

1. Fork本仓库
2. 创建特性分支
3. 提交更改
4. 发起Pull Request

## 📖 参考资料

- [PPO论文](https://arxiv.org/abs/1707.06347)
- [DPO论文](https://arxiv.org/abs/2305.18290)
- [GRPO论文](https://arxiv.org/abs/2305.18290)
- [RLHF综述](https://arxiv.org/abs/2309.00770)

## 📝 引用

如果您在研究中使用了本项目，请引用：

```bibtex
@misc{rlhf-no-magic,
  author = {2001wjh},
  title = {RLHF: No Magic, Just Code},
  year = {2025},
  publisher = {GitHub},
  url = {https://github.com/2001wjh/RLHF-No-Magic-Just-Code}
}
```

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## ⭐ Star History

[![Star History Chart](https://api.star-history.com/svg?repos=2001wjh/RLHF-No-Magic-Just-Code&type=Date)](https://star-history.com/2001wjh/RLHF-No-Magic-Just-Code&Date)

