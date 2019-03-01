---
title: "Monocular Camera Based Fruit Counting and Mapping with Semantic Data Association"
collection: publications
permalink: /publication/ral_mono_fruit_2019.md
excerpt: 'We present a cheap, lightweight, and fast fruit counting pipeline. Our pipeline relies only on a monocular camera..'
date: 2019-02-28
venue: ' IEEE Robotics and Automation Letters (27 February 2019) '
paperurl: 'https://ieeexplore.ieee.org/document/8653965/'
citation: 'Liu, Xu. (2019). &quot;Monocular Camera Based Fruit Counting and Mapping with Semantic Data Association&quot; <i>Journal 1</i>. 1(3).'
---

We present a cheap, lightweight, and fast fruit counting pipeline. Our pipeline relies only on a monocular camera, and achieves counting performance comparable to a state-of-the-art fruit counting system that utilizes an expensive sensor suite including a monocular camera, LiDAR and GPS/INS on a mango dataset. Our pipeline begins with a fruit and tree trunk detection component that uses state-of-the-art convolutional neural networks (CNNs). It then tracks fruits and tree trunks across images, with a Kalman Filter fusing measurements from the CNN detectors and an optical flow estimator. Finally, fruit count and map are estimated by an efficient fruit-as-feature semantic structure from motion (SfM) algorithm which converts 2D tracks of fruits and trunks into 3D landmarks, and uses these landmarks to identify double counting scenarios. There are many benefits of developing such a low cost and lightweight fruit counting system, including applicability to agriculture in developing countries, where monetary constraints or unstructured environments necessitate cheaper hardware solutions.

[Download paper here](https://ieeexplore.ieee.org/document/8653965/)

Recommended citation: X. Liu et al., "Monocular Camera Based Fruit Counting and Mapping with Semantic Data Association," in IEEE Robotics and Automation Letters.
doi: 10.1109/LRA.2019.2901987
