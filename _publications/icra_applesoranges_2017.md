---
title: "Counting Apples and Oranges with Deep Learning: A Data-Driven Approach"
collection: publications
permalink: /publication/icra_applesoranges_2017
excerpt: 'This paper describes a fruit counting pipeline based on deep learning that accurately counts fruit in unstructured environments'
date: 2017-01-11
venue: ' IEEE Robotics and Automation Letters (Volume: 2, Issue: 2, April 2017)'
paperurl: 'https://ieeexplore.ieee.org/abstract/document/7814145/'
citation: 'Chen, S.W. (2017). &quot;Counting Apples and Oranges with Deep Learning: A Data-Driven Approach&quot; <i>Journal 1</i>. 1(2).'
---
This paper describes a fruit counting pipeline based on deep learning that
accurately counts fruit in unstructured environments. Obtaining reliable fruit
counts is challenging because of variations in appearance due to illumination
changes and occlusions from foliage and neighboring fruits. We propose a novel
approach that uses deep learning to map from input images to total fruit counts.
The pipeline utilizes a custom crowdsourcing platform to quickly label large
data sets. A blob detector based on a fully convolutional network extracts
candidate regions in the images. A counting algorithm based on a second
convolutional network then estimates the number of fruits in each region.
Finally, a linear regression model maps that fruit count estimate to a final
fruit count. We analyze the performance of the pipeline on two distinct data
sets of oranges in daylight, and green apples at night, utilizing human
generated labels …

[Download paper here](https://ieeexplore.ieee.org/abstract/document/7814145/)

Recommended citation: Chen, S.W., Shivakumar, S.S., Dcunha, S., Das, J., Okon, E., Qu, C., Taylor, C.J. and Kumar, V., 2017. Counting apples and oranges with deep learning: A data-driven approach. IEEE Robotics and Automation Letters, 2(2), pp.781-788.
