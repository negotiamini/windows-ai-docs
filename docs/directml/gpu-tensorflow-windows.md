---
title: TensorFlow with DirectML on Windows
description: Enable TensorFlow with DirectML directly on Windows
ms.topic: article
ms.date: 06/17/2020
---

# Enable TensorFlow with DirectML on Windows

This release provides students, beginners, and professionals a way to run machine learning (ML) training on their existing hardware by using the TensorFlow with DirectML package. Once set up, you can use your exisiting model scripts or check out a few [samples on the DirectML repo](https://github.com/microsoft/DirectML/tree/master/TensorFlow). 

## Check your version of Windows 

The **TensorFlow with DirectML** package on native Windows works starting with Windows 10, version 1709 (Build 16299 or higher). You can check your build version number by running `winver` via the **Run** command (Windows logo key + R).

## Check for GPU driver updates 

Ensure that you have the latest GPU driver installed. Select **Check for updates** in the **Windows Update** section of the **Settings** app.

## Set up TensorFlow with DirectML 

We recommend setting up a virtual Python environment inside Windows. There are many tools that you can use to set up a virtual Python environment&mdash;for these instructions, we'll use [Anaconda's Miniconda](https://docs.conda.io/en/latest/miniconda.html). The rest of this setup assumes that you use a Miniconda environment. 

### Set up Python environment 

Download and install the [Miniconda Windows installer](https://docs.conda.io/en/latest/miniconda.html#windows-installers) on your system. There is [additional guidance for setup](https://conda.io/projects/conda/en/latest/user-guide/install/windows.html) on Anaconda's site. Once Miniconda is installed, create an environment using Python named **directml**, and activate it through the following commands.

> [!NOTE]
> In the commands below, we use Python 3.6. However, the tensorflow-directml package works in a Python 3.5, 3.6, or 3.7 environment. 

```
conda create --name directml python=3.6 

conda activate directml 
```

### Install the TensorFlow with DirectML package 

Install the TensorFlow with DirectML package through *pip* by running the following command.

> [!NOTE]
> The tensorflow-directml package supports only TensorFlow 1.15. 

```
pip install tensorflow-directml
```

Once you've installed the *tensorflow-directml* package, you can verify that it runs correctly by adding two tensors. Copy the following lines into an interactive Python session.

```
import tensorflow.compat.v1 as tf 

tf.enable_eager_execution(tf.ConfigProto(log_device_placement=True)) 

print(tf.add([1.0, 2.0], [3.0, 4.0])) 
```

You should see output similar to the following, with the *add* operator placed on the DML device. 

```
2020-06-15 11:27:18.235973: I tensorflow/core/common_runtime/dml/dml_device_factory.cc:45] DirectML device enumeration: found 1 compatible adapters. 

2020-06-15 11:27:18.240065: I tensorflow/core/common_runtime/dml/dml_device_factory.cc:32] DirectML: creating device on adapter 0 (AMD Radeon VII) 

2020-06-15 11:27:18.323949: I tensorflow/stream_executor/platform/default/dso_loader.cc:60] Successfully opened dynamic library DirectMLba106a7c621ea741d2159d8708ee581c11918380.dll 

2020-06-15 11:27:18.337830: I tensorflow/core/common_runtime/eager/execute.cc:571] Executing op Add in device /job:localhost/replica:0/task:0/device:DML:0 

tf.Tensor([4. 6.], shape=(2,), dtype=float32) 
```

## TensorFlow with DirectML samples and feedback 

Check out [our samples](https://github.com/microsoft/DirectML/tree/master/TensorFlow) or utilize your exisiting model scripts. If you run into issues or have feedback on the TensorFlow with DirectML package, then please [connect with our team](https://github.com/microsoft/tensorflow-directml/issues). 
