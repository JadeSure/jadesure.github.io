---
layout:     post
title:      Recommendation System for News DAY2
subtitle:   Data Analysis (Data exploration)
date:       2020-11-27
author:     Shuo Wang
header-img:  img/post-bg-swift2.jpg
catalog: true
tags:
    - recommendation system
    - news
    - visualization 
---

# Data description
four files:
- article.csv includes article attributes (article id, category id, time stamp, words count)
- article_emb.csv includes article embedding with (totally 250 ways)
- train_click_log.csv includes user id, click article

# Relative package
- only predict the last article news
- convert log info to: features + labels(click on the probability, then, it is a classification question)

```python
import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns
plt.rc('font', family='SimHei', size=13)

import os,gc,re,warnings,sys
# omit python warning which is caused by different software versions
warnings.filterwarnings('ignore')

```


```python
path = './data_raw/'
```

To be continue...
