# Transfer Learning

When performing BBO, users often run tasks that are similar to
previous ones. This observation can be used to speed up the current task.
Compared with Vizier, which only provides limited transfer learning
functionality for single-objective BBO problems, OpenBox employs
a general transfer learning framework with the following
advantages:

1) Support for generalized black-box optimization problems;

2) Compatibility with most Bayesian optimization methods.

OpenBox takes as input observations from 𝐾 + 1 tasks: D<sup>1</sup>, ...,
D<sup>𝐾</sup> for 𝐾 previous tasks and D<sup>𝑇</sup> for the current task. 
Each D<sup>𝑖</sup> = {(𝒙, 𝒚)},
𝑖 = 1, ...,𝐾, includes a set of observations. Note that,
𝒚 is an array, including multiple objectives for configuration 𝒙.
For multi-objective problems with 𝑝 objectives, we propose to
transfer the knowledge about 𝑝 objectives individually. Thus, the
transfer learning of multiple objectives is turned into 𝑝 single-objective
transfer learning processes. For each dimension of the
objectives, we take the following transfer-learning technique:

1) We first train a surrogate model 𝑀<sup>𝑖</sup> on 𝐷<sup>𝑖</sup> for the 𝑖-th prior task
and 𝑀<sup>𝑇</sup> on 𝐷<sup>𝑇</sup>; 

2) Based on 𝑀<sup>1:𝐾</sup> and 𝑀<sup>𝑇</sup>, we then build a transfer learning surrogate by combining all base surrogates:
𝑀<sup>TL</sup> = agg({𝑀<sup>1</sup>, ...,𝑀<sup>𝐾</sup>,𝑀<sup>𝑇</sup> };w);

3) The surrogate 𝑀<sup>TL</sup> is used to guide the configuration search,
instead of the original 𝑀<sup>𝑇</sup>. 

Concretely, we use gPoE to combine the multiple base surrogates (agg), 
and the parameters w are calculated based on the ranking of configurations, 
which reflects the similarity between the source tasks and the target task.


## Performance Comparison
We compare OpenBox with a competitive transfer learning baseline Vizier and a non-transfer baseline SMAC3. 
The average performance rank (the lower, the better) of each algorithm is shown in the following figure. 
For experimental setups, dataset information and more experimental results, please refer to our [published article]().


<p align="center">
<img src="https://raw.githubusercontent.com/PKU-DAIR/open-box/master/docs/imgs/tl_lightgbm_75_rank_result.svg" width="70%">
</p>
