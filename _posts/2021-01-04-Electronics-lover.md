---
layout:     post
title:      Electronics Lover
subtitle:   It includes assembling, maintenance, fixing problems for PC, iPhone; Rebuild and be familiar with operation system, such as Linux, MacOS and Windows; Build firewall for Internet bar to avoid ip flooding.
date:       2021-01-04
author:     Shuo Wang
header-img: img/computers_phones/post-bg-aircraft.JPG
catalog: true
tags:
    - PC
    - Phones
    - System
    - Linux
    - MacOS
    - Windows
    - Virtual Machine
    - Network
---


# Install TensorFlow-GPU by Anaconda (conda install tensorflow-gpu)

It might be the simplest way to install Tensorflow or Tensorflow-GPU by conda install in the conda environment  
--

Nowadays, there are many tutorials that instruct how to install tensorflow or tensorflow-gpu. However, some people may feel it too complex just like me, because in those ways, you should download and install [NVIDIA drivers](https://www.nvidia.com/Download/index.aspx?lang=en-us), and then download and install [CUDA](https://developer.nvidia.com/cuda-downloads) (users need to pay attention to the version), afterwards you may sign an agreement and download cuDNN in [NVIDIA Developer](https://developer.nvidia.com/cudnn). Next, install python, and pip install tensorflow-gpu and so on. It's not esay for developer to do these, let alone it might causes some other error such as **version not match**, or **conflict between other python libraries** and so on. Moreover, if you want to [install tensorflow by compilation](https://www.tensorflow.org/install/gpu), it may take much more time.  

Thus I strongly reconmend you not to do this, there's a much easier way to install this. Please read the following article.

---

## Install Anaconda
>[Anaconda](https://www.anaconda.com/) is a free and open-source distribution of the Python and R programming languages for scientific computing, that aims to simplify package management and deployment.   

**You can download anaconda [here](https://www.anaconda.com/distribution/#download-section).**

One of the advantage of anaconda is that it can create **isolated environment** in your device, and you can configure any libraries and toolkits in the 'env' without affect other environment. Once you are nor satisfied of your configuration, you can simplily delete the environment.

Note that in you are in **China**, download anaconda might take a long time due to some resons that cannot say. Instead, you can download it from [**Tsinghua mirror**](https://mirror.tuna.tsinghua.edu.cn/help/anaconda/), and install it **manually**.  

After downloading this successfully, try to run the installation file.
For example, if you use ubuntu, you can cd to the path of the sh file and run the following command:

```bash
./Anaconda3-5.3.1-Linux-x86_64.sh
```
***Attention that you should change the command above to your own installation file name.***

Then you will successfully install Anaconda!

## Create new environment by conda

If you are unwilling to create conda environment (maybe because of lazy), you can skip this section. However, I strongly reconmend you to create this **for the convience in the future**.  

Run the command below:
```bash
conda create -n tf
```
![picture1](/img/computers_phones/1.jpg)

'tf' is the name of your new conda environment, you can try other names as your own interest.

For other management you conda env, you can read [this](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html?highlight=environment).

## Install Tensorflow

