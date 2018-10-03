---
title: 'Jetson Xavier - Initial Thoughts'
date: 2018-10-3
permalink: /posts/jetsonxavier-initialthoughts/
tags:
  - embedded
  - gpu
  - robotics
  - computer vision
  - nvidia
---

Ever since the Jetson Xavier was announced, I've been itching to get my hands on
one of them to put it through it's paces. Thanks to James over at [Ghost
Robotics](https://www.ghostrobotics.io/) I finally get to play with one of
these. I've spent a fair amount of time with the Jetson TX1 and Jetson TX2 and I
will be making direct comparisons to the Xavier's predecessor, the TX2.

Hardware and Design
======

Out of the box, the Xavier devkit in no way resembles the previous devkits, and
that's a good thing because the previous dev kits had limited to no practical
value for what we use them for (mobile robots -
[Falcon 250](https://osrf.github.io/ovc/assets/images/ovc1-drone.png) +
[Open Vision Computer](http://open.vision.computer)).
The entire physical footprint of the devkit is slightly larger than the actual module, and it appears that it couldn't
get much smaller even in a tightly packed carrier board (good job @nvidia). However, the first
reaction is to the weight of this unit. It weighs roughly __660gms__ out of the box,
without the power supply. Since this is a loaner unit and since I cannot gut the
thing yet, I will guesstimate that most of this weight is the extremely heavy
heat sink and casing. I will update this post once I get my own unit and take
all of that off! The unit is a bit tall too but it's mostly 70% heatsink and fan
enclosure.

__Figure 1: TX2 devkit vs Xavier devkit__ (food truck cash card for size comparison)
![devkit-comparisons-1](/images/IMG_3345.jpg)
__Figure 2: Height Comparison__
![devkit-comparisons-2](/images/IMG_3346.jpg)
__Figure 3: The incredible bulk__
![xavier-weight](/images/IMG_3344.jpg)
__Figure 4: Dimensions__
![xavier-height](/images/IMG_3352.jpg)
__Figure 5: Dimensions__
![xavier-width](/images/IMG_3347.jpg)
__Figure 6: Under the carrier hood__
![xavier-carrier](/images/IMG_3349.jpg)
__Figure 7: Power suply__
![xavier-ps](/images/IMG_3354.jpg)

Adding to the good news, this product seems well build and extremely well protected.
If weight isn't a problem, I would strap one of these onto a robot directly
without the hassle of manufacturing or buying a separate carrier board.

I would have liked if there was at least another USB Type A port. The
eSATAp+USB3.0 TypeA port is cool but I think most robotics peripherals are still
on Type A and I would have preferred not to bring the battle of dongles into the
robotics world, but oh well. The kind folks at NVIDIA do ship the devkits with
USB-C to Type-A dongles and don't charge you extra for it (take that @apple).
Apart from the USB-C, the rest of the I/O is similar to the TX2 dev-kits. There's an
additional M2 which will definitely prove usefull. For those that care, the
power supply adapter is now a bit smaller too. Now, onto the fun stuff..

Specifications and Performance
======

__CUDA Compatibility Major/Minor version number: 7.2__

__Multiprocessors: 8__ (TX2 has 2)

__CUDA Cores/Mp: 64__ (TX2 has 128)

__Total CUDA Cores: 512__ (TX2 has 256)

__Global Memory: ~16GB__ (TX2 has ~8GB)

__GPU Max Frequency: 1500GHz__ (TX2 has 1300GHz)

__Memory Clock Rate: 1500MHz__

__Memory Bus Width: 256-bit__ (TX2 has 128-bit)

__Figure 8: Device Query__
![device-query](/images/device_query.png)

The CUDA Cores to Multiprocessor ratio is interesting. I will post a more
detailed follow up with actual benchmarks on my code soon. I suspect the Xavier
will be able to better handle multiple CUDA streams and kernel launches because
of this, and that is exciting.

In the CPU realm, the Xavier brings 8 ARMv8 Processor cores, which seem to perform significantly
better than the TX2, where the Denver cores didn't really make significant
contributions to performance. The CPU max frequency is 2265Hz and I did a little
stress test to see how hot things could get.

```
sudo ./jetson_clocks
```

Here is somewhat of a baseline for CPU and GPU temperatures. The device was
idling when these were recorded. These are not freshly booted temperatures.
Those are in the late 30 degres celsius range.

__Figure 8: Before CPU stress test:__
![thermal-baseline](/images/baseline_perf_thermal.png)

Let's stress it out:
```
stress --cpu 8 --io 6 --vm 6 --vm-bytes 2048M --timeout 600s
```

__Figure 9: Stress temperatures:__
![thermal-cpu](/images/stress_temp.png)

CPU-bound processes seem to be handled fairly well. I ran the stress test for 10
minutes each a few times and temperatures stayed in the 50s.


To add some fuel to the fire, I threw in a pretty intensive GPU-bound process to
the mix (and dialed back the CPU stress io and vm parameters to 2).
```
./nbody_opengles -benchmark -fp64 -fullscreen -numbodies=1000000
```

__Figure 10: GPU Stress temperatures:__
![hot-hot-hot](/images/cpugpumax.png)

Things got hot. Both CPU and GPU internal temperatures began to cross the 70
degree mark. Temperatures remained in the 70s and didn't appear to increase much
even at 100% CPU and 100% GPU usage.

While the devkit seems to be well cooled, I suspect the Xavier will not take
well to having it's heatsink, fan and casing thrown away (as we bravely do with
the Falcon 250, but that is an experiment I still intend on performing).

Final Thoughts
======

30-10-02: I think this is a great step forward when compared to the TX2 devkits.
Performance out of the box is impressive. A proper benchmark on existing TX2
code is next on the to-do list along with a more comprehensive thermal analysis
experiment without the fan and heat sink.

