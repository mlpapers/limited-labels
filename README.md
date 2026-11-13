# Learning with Limited Labels

When labels are scarce or unreliable, learning depends on which examples get labeled and what can be inferred from the rest. This review covers semi-supervised learning, active label acquisition, positive-unlabeled data and weak or noisy supervision. Adapting pretrained models belongs in [Transfer Learning](https://mlpapers.org/transfer-learning/), and learning to adapt across tasks in [Meta-Learning](https://mlpapers.org/meta-learning/).

## Learning from labeled and unlabeled examples

- **Harmonic label propagation** - Places labeled and unlabeled examples on a similarity graph. Fixing the labeled values, the remaining predictions minimize graph energy and equal weighted averages of their neighbors. The graph encodes the assumption that nearby examples share labels. [Zhu et al. 2003](<https://pages.cs.wisc.edu/~jerryzhu/pub/zgl.pdf> "Semi-Supervised Learning Using Gaussian Fields and Harmonic Functions; ICML").
- **Mean Teacher** - Averages model weights to produce teacher targets for consistency training on perturbed inputs. This uses unlabeled observations during fitting; its benefit depends on the architecture and the relation between labeled and unlabeled data. [Tarvainen and Valpola 2017](<https://arxiv.org/abs/1703.01780> "Mean teachers are better role models: Weight-averaged consistency targets improve semi-supervised deep learning results; NeurIPS").
- **MixMatch** - Averages predictions across augmented unlabeled images, sharpens the targets and mixes labeled and unlabeled examples with MixUp. On CIFAR-10 with 250 labels, test error is about 11% versus 38% for the reported prior best. [Berthelot et al. 2019](<https://proceedings.neurips.cc/paper_files/paper/2019/hash/1cd138d0499a68f4bb72bee04bbec2d7-Abstract.html> "MixMatch: A Holistic Approach to Semi-Supervised Learning; NeurIPS").
- **FixMatch** - Uses confident predictions on weakly augmented unlabeled images as targets for strongly augmented versions. Combines pseudo-labeling with consistency; the confidence threshold and augmentation policy determine which unlabeled evidence enters training. [Sohn et al. 2020](<https://arxiv.org/abs/2001.07685> "FixMatch: Simplifying Semi-Supervised Learning with Consistency and Confidence; NeurIPS").
- **Learning from multiple views** - See [Multi-View Learning](https://mlpapers.org/multiview-learning/) for co-training and assumptions about complementary views.

## Choosing which examples to label

- **BALD active learning** - Chooses labels expected to reduce posterior uncertainty about the model, using disagreement among predictive distributions. Houlsby et al. derive it for Gaussian-process classification; querying labels differs from passive few-shot adaptation. [Houlsby et al. 2011](<https://arxiv.org/abs/1112.5745> "Bayesian Active Learning for Classification and Preference Learning; arXiv").
- **TypiClust** - Selects typical examples from diverse clusters in self-supervised representations. At very small image-label budgets it beats tested uncertainty-based strategies. Experiments and a mixture-model analysis show that the preferred strategy changes with budget. [Hacohen et al. 2022](<https://proceedings.mlr.press/v162/hacohen22a.html> "Active Learning on a Budget: Opposite Strategies Suit High and Low Budgets; ICML").

## Selective, weak and noisy labels

- **Positive-unlabeled learning** - Learns from known positives and an unlabeled mixture of both classes. If labeled positives are selected uniformly within their class, label probability is proportional to class probability; selective labeling breaks this correction. [Elkan and Noto 2008](<https://cseweb.ucsd.edu/~elkan/posonly.pdf> "Learning Classifiers from Only Positive and Unlabeled Data; KDD").
- **Class-conditional loss correction** - With known class-specific label-flip rates, transforms a binary loss so its expectation equals the clean-label loss. Assumes independent flips within each class and rates summing to less than one. [Natarajan et al. 2013](<https://proceedings.neurips.cc/paper_files/paper/2013/hash/3871bd64012152bfb53fdf04b401193f-Abstract.html> "Learning with Noisy Labels; NeurIPS").
- **Programmatic weak supervision** - Snorkel combines noisy labeling functions into probabilistic training labels by modeling their accuracies and dependencies, then trains a discriminative model. Development and test sets remain labeled. [Ratner et al. 2017](<https://pmc.ncbi.nlm.nih.gov/articles/PMC5951191/> "Snorkel: Rapid Training Data Creation with Weak Supervision; PVLDB").
- **Confident Learning** - Uses out-of-sample probabilities to estimate the joint distribution of observed and latent labels and rank suspected errors. Assumes class-conditional label noise; exact recovery also needs constraints on prediction errors. [Northcutt et al. 2021](<https://arxiv.org/abs/1911.00068v6> "Confident Learning: Estimating Uncertainty in Dataset Labels; JAIR"); [code](<https://github.com/cleanlab/cleanlab>).

## Comparative evidence

- **Semi-supervised evaluation** - Oliver et al. find that out-of-class unlabeled examples can degrade tested methods and that strong supervised baselines are often underreported. Match backbones and label-selection budgets; more unlabeled data need not improve performance. [Oliver et al. 2018](<https://arxiv.org/abs/1804.09170> "Realistic Evaluation of Deep Semi-Supervised Learning Algorithms; NeurIPS").

## Related topics

- [Transfer Learning](https://mlpapers.org/transfer-learning/)
- [Meta-Learning](https://mlpapers.org/meta-learning/)
- [Feature Extraction](https://mlpapers.org/feature-extraction/)
- [Multi-View Learning](https://mlpapers.org/multiview-learning/)
- [Model Evaluation](https://mlpapers.org/evaluation/)
