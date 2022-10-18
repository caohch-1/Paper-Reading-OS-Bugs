# Paper-Reading-OS-Bugs
 简单记录一下读过的OS-Bugs相关比较有意思的paper，方便以后要用的时候找到

## Correlating instrumentation data to system states- A building block for automated diagnosis and control (OSDI2004)
### New concepts
- Service Level Objectives(SLOs): [SLI, SLO, and SLA Difference](https://ikala.cloud/understanding-sli-slo-sla-in-sre/)
- Three-tier Web Service: [Three-tier Arch.(1)](https://www.ibm.com/hk-en/cloud/learn/three-tier-architecture), [Three-tier Arch.(2)](https://www.techtarget.com/searchsoftwarequality/definition/3-tier-application)
- Tree-augmented naive Bayesian network (TAN): [NB vs. TAN](https://gmis.jiqizhixin.com/graph/technologies/f743c6ed-68c5-4cc1-963f-c66413733e6e)
- TBD


### Notes
- 目的是做一个分类器，输入是系统的一些运行时信息(metrics)，输出是系统的SLO是否被违背；
- 借助于TANs作为分类器所带来的可解释性，我们也得以发现SLO违背与哪部分metrics有关，以及metrics对应的阈值，换而言之能够发现引起SLO违背的表面原因；
- 由于metrics与系统组件有关(i.e., 你考试没考好你爸打你而不是隔壁王叔叔打你)，我们能够进一步推断系统的哪些组件、资源或进程导致了SLO违背，换而言之能够发现引起SLO违背的根本位置与原因；
- 使用balanced accuracy (BA)而非普通的accuracy(i.e., 这里有歧义，作者这里其实指代的是只考虑TP的precision，现在用于模型评估的accuracy与作者提出的BA类似也同时考虑TP和TN，参考[混淆矩阵的相关概念](https://blog.csdn.net/qq_38436431/article/details/120538673))来进行评估，BA其实就是$\frac{TP+TN}{2}$；
- 得到分类器后通过判断$P(s^+|\vec{M})>P(s^-|\vec{M})$来判断输入的sub-metrics与SLO违背是否有强的联系，有点怪因为这应该与sub-metrics中的具体取值有关，但是 intuitively符合理解；
- TBD