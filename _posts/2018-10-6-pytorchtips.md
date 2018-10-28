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

__2. Transferring Weights and Distributed Training__

I use different shared machines with multiple GPUs and often use different GPU
ids on different days based on availability. I also occasionally switch between
multi-gpu training and single-gpu training etc. I noticed that the
**nn.DataParallel** class can be a bit tricky to navigate for such usage
conditions, specially if you're not aware of how models are saved to file, which
I wasn't at the time.

If you're training a model on a multi-gpu setup and save the model naively, you
are unknowingly appending a "module" tag to the *state_dict* elements present in
the model parameters key-value store, and it appears that this assumes some
implicit binding to specific GPUs (I could be wrong?). But if you naively try to
load and run this model on a different multi-gpu setup, you will notice an error
that says a specific tensor is meant to run on a specific GPU. We don't want
that.

What the error message looks like:
```
RuntimeError: Expected tensor for argument #1 'input' to have the same device as
tensor for argument #2 'weight'; but device 0 does not equal 1 (while checking
arguments for cudnn_convolution)
```

The easiest suggested fix is to iterate through the model *state_dict* key-value
store and remove the "module." binding like this:
```
pretrained_model = checkpoint['model']
new_model = SomeNetwork()
from collections import OrderedDict
new_model_dict = OrderedDict()
for k,v in pretrained_model.state_dict().items():
    # Drop the "Module." characters from the name
    name = k[7:]
    new_model_dict[name] = v
new_model.load_state_dict(new_model_dict)

```

[Credit](https://discuss.pytorch.org/t/solved-keyerror-unexpected-key-module-encoder-embedding-weight-in-state-dict/1686/2)
