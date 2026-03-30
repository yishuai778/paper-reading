# Output Formats

Use the lightest format that matches the user's request. Keep outputs compact by default and expand only when the user asks for depth.

## 1. Quick Read

Use for triage, first pass, or "值不值得看".

```markdown
## 一句话判断
[用一句话说明这篇论文在做什么，以及值不值得继续读]

## 核心内容
- 问题：
- 贡献：
- 方法：
- 证据：

## 为什么重要
- [对研究或工程的实际意义]

## 最大疑点
- [最值得警惕的一点]

## 建议动作
- [继续精读 / 只记概念 / 看基线 / 不建议投入]
```

## 2. Deep Read

Use when the user wants a full paper breakdown.

```markdown
## 论文定位
- 题目：
- 类型：
- 要解决的问题：
- 论文一句话 thesis：

## 贡献拆解
- 贡献 1：
- 贡献 2：
- 贡献 3：

## 方法机制
1. 输入是什么
2. 中间关键步骤是什么
3. 训练/推理时怎样工作
4. 输出是什么

## 实验与证据
- 数据/benchmark：
- 指标：
- 主要 baseline：
- 最关键结果：
- ablation 是否支撑 claim：

## 我怎么判断
- 可信之处：
- 薄弱之处：
- 隐含假设：
- 外部有效性：

## 对你的价值
- 值得借鉴的点：
- 不必照搬的点：
- 如果要复现，先做什么：
```

## 3. Comparison Read

Use when the user gives multiple papers.

Start with a compact comparison table, then explain the decisive differences.

Recommended columns:

| Paper | Problem | Core idea | Data / Benchmark | Evidence quality | Main limitation | When to use |
| --- | --- | --- | --- | --- | --- | --- |

Then add:

```markdown
## 关键差异
- 方法差异：
- 评测差异：
- 适用场景差异：

## 谁更适合作为主参考
- [paper]
- 原因：

## 组合阅读顺序
1. [paper]
2. [paper]
3. [paper]
```

## 4. Literature Seed Map

Use for mini-surveys or topic onboarding.

```markdown
## 主题切分
- 子方向 A：
- 子方向 B：
- 子方向 C：

## 代表论文
- [paper]：为什么关键
- [paper]：为什么关键

## 推荐阅读顺序
1. 先读：
2. 再读：
3. 最后读：

## 当前空白
- 哪些问题还没解决
- 哪些 benchmark 可能不够真实
- 哪些结论还不稳
```

## 5. Reproduction Memo

Use when the user wants implementation value, not just understanding.

```markdown
## 复现目标
- 精确复现 / 方向性复现 / 只复现核心机制

## 必需资源
- 数据：
- 模型：
- API / 工具：
- 算力：
- 评测脚本：

## 高风险缺口
- [论文未交代清楚的点]

## 建议实施路径
1. 先搭最小闭环
2. 再补齐 benchmark / 工具 / 数据
3. 最后追结果

## 预期难度
- 低 / 中 / 高
- 原因：
```

## Evidence Markers

When useful, tag statements inline:

- `论文明确说明` for direct claims from the source
- `合理推断` for inference based on the source
- `论文未说明` for missing but important details

Use these markers sparingly but clearly, especially in reproduction and critique outputs.
