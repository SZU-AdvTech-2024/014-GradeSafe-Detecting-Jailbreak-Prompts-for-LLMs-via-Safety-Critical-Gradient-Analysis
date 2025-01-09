## 概述
大语言模型 (LLMs) 正在面临越狱提示的威胁。现有的越狱提示方法主要是使用在线审核 API 或微调的 LLM 进行检测。然而，这些方法往往需要进行大量的的数据收集和训练。在这篇文章中，作者提出了 GradSafe，它通过仔细检查 LLMs 中安全关键参数的梯度来有效地检测越狱提示。该方法基于一个关键的观察：在某些安全关键参数上，LLM对越狱提示的损失梯度与顺从反应的梯度显示出相似的模式。相比之下，安全提示导致不同的梯度模式。基于这一观察，GradSafe 分析了 (与顺从反应配对) 提示的梯度，以准确检测越狱提示。这篇文章证明，无需进一步训练，将 GradSafe 应用于 Llama-2 上，其性能优于 Llama Guard，其中 Llama Guard 是在检测越狱提示的大数据集上进行了广泛的微调的 LLM。这种优异的性能在 zero-shot 和适应场景下都是一致的，对 ToxicChat 和 XSTest 的评估证明了这一点。


## 数据集

ToxicChat数据集在 https://huggingface.co/datasets/lmsys/toxic-chat 下载，使用toxicchat1123进行评估

XSTest数据集在 https://huggingface.co/datasets/natolambert/xstest-v2-copy 

下载数据集然后保存在./data下

## 基座模型

从 https://huggingface.co/meta-llama/Llama-2-7b-chat-hf 下载Llama-2 7b，然后保存在./model

## 评估

使用以下两个命令评估GradSafe性能：

> python ./code/test_xstest.py

> python ./code/test_toxicchat.py



