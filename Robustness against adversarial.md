---
title: "Recent Developments in Deep Learning: Robustness against Adversarial"
author:
    - Yuhao Wang
preliminary: true
autoSectionLabels: true
cref: true
---

#### Abstract

This project sum up the main points of the recent developments in deep learning for robustness against adversarial perturbation, then elaborated the tasks, datasets, evaluations of the previous approache adversarial training and the state of the art parseval regularization. Furthermore made a detailed comparsion of the previous method and the most advanced approach. Through the summary from this project want to provide more new thoughts and directions for future work.

## Introduction

In the past few decades, with the rapid development of the Machine Learning and Deep Learning, the application of these technology has become increasingly prosperous worldwide. However at the same time many data scientist have found: Even examples have only subtle different from the truely examples drawn from the data distributions, they might also be missclassified by particular deep learning models. Early people attempts to explain these phenomenon with their overfitting and nonlinearity, but Goodfellow et al.(2015) argue instead that the primary cause of neural networks' vulnerability to adversarial perturbation is their linear nature, moreover their explanation is verified by quantitative results. 

In oder to resist adversarial perturbation Goodfellow et al.(2015) suggested training on adversarial examples to regualrize the model. But limited by the expensive constrained optimization in the inner loop, this method can not efficient be used in the model training procedure. Later Moustapha et al.(2017) advised a new approach Parseval Networks to improve robustness to adversarial examples. In this parseval networks weight matrices of linear and convolutional layers are maintained to be Parseval tight frames, which are extensions of orthogonal matrices to non-square matrices.