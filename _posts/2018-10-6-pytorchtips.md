---
title: 'Pytorch Scribbles'
date: 2018-10-6
permalink: /posts/pytorch_notes/
tags:
  - gpu
  - robotics
  - computer vision
  - deep learning
  - pytorch
---

PyTorch Scribble Pad
======

This page is a collection of notes and tips for myself in getting familiar with
the workings of PyTorch.

__1. Transfering Weights__

If you have a pretrained network A with some layers A:{x,y,z} and you have a new
network architecture with some layers B:{w,x,y,z,a}, and you wish to transfer
weights learned from network A for layers {x,y,z} to B, you can do it using the
following:

```
pretrained_model_weights = torch.load('../path/model.pth')
new_model_weights = model.state_dict()
pretrained_model_weights = {k: v for k, v in pretrained_model_weights.items() if k in new_model_weights}
new_model_weights.update(pretrained_model_weights)
model.load_state_dict(new_model_weights)
```

