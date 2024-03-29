# Demo

[![arXiv](https://img.shields.io/badge/arXiv-2011.03870-green.svg)](https://arxiv.org/abs/2011.03870)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/neemakot/Fact-Checking-Survey)
[![Last Commit](https://img.shields.io/github/last-commit/neemakot/Fact-Checking-Survey.svg)](https://github.com/neemakot/Fact-Checking-Survey)
[![Contribution_welcome](https://img.shields.io/badge/Contributions-welcome-blue)](https://github.com/neemakot/Fact-Checking-Survey/blob/main/CONTRIBUTING.md)


This is the official repository of the paper:

> **Mining Dual Emotion for Fake News Detection.** [[PDF]](https://www.zhangxueyao.com/assets/www2021-dual-emotion-paper.pdf) [[Code]](https://github.com/RMSnow/WWW2021) [[Slides]](https://www.zhangxueyao.com/assets/www2021-dual-emotion-slides.pdf) [[Video]](https://www.zhangxueyao.com/assets/www2021-dual-emotion-video.mp4) [[中文讲解视频]](https://www.bilibili.com/video/BV13o4y1m7c3)
>
> Xueyao Zhang, Juan Cao, Xirong Li, Qiang Sheng, Lei Zhong, and Kai Shu. Proceedings of 30th The Web Conference (**WWW 2021**)

## Datasets

The datasets are available at https://drive.google.com/drive/folders/1pjK0BYiiJt0Ya2nRIrOLCVo-o53sYRBV?usp=sharing. The downloaded datasets (i.e., the  `dataset` folder) need to be moved into the root path of this project.

Our experimental dataset is in the folder `dataset/RumourEval-19`, which contains three json files. In every json file,

- the `id` identifies the unique id of the post.
- the `label` identifies the veracity of the post, whose value ranges in [ `fake`,  `real`, `unverified`]. 
- the `content` is the content of the post.
- the `comments` are the users' comments list towards the post.
- the `content_emotions_labels` and `cotent_emotions_probs` are the *Emotion Category* features of the content. And the `comments100_emotions_labels_mean_pooling`, `comments100_emotions_labels_max_pooling`, `comments100_emotions_probs_mean_pooling`, and `comments100_emotions_probs_max_pooling` are the *Emotion Category* features of the earliest 100 comments. The way how to use these features will be described in [here](https://github.com/RMSnow/WWW2021#step12-get-the-emotion-features).

Here is an overview of papers mentioned in this work, and more recent papers which have been added.

- [Introduction](#introduction)
- [Task Formulations](#task-definitions)
- [Datasets](#fact-checking-datasets)
  - [Naturally occurring claims](#datasets-of-naturally-occurring-claims)
    - [From social media](#social-media)
    - [From fact-checking and news websites](#fact-checking-and-news-websites)
  - [Hand crafted claims](#hand-crafted)
    - [From Wikipedia](#wikipedia)
    - [From scientific journals](#scientific-journals)
- [Fact Checking Systems](#fact-checking-systems)
  - [By dataset](#systems-by-dataset)
    - [LIAR dataset](#liar)
    - [FEVER dataset](#fever)
    - [MultiFC dataset](#multifc)
  - [By method](#systems-by-method)
    - [Support Vector Machines (SVMs)](#support-vector-machines)
    - [Convolutional Neural Networks (CNNs)](#convolutional-neural-networks)
    - [Recurrent Neural Networks (RNNs)](#recurrent-neural-networks)
    - [Attention Networks](#transformers-and-attention-networks)
    - [Hybrid](#hybrid)
- [Shared Tasks](#shared-tasks)

## Emotion Resources

| Type                    | Language | Resources                                                    |
| ----------------------- | -------- | ------------------------------------------------------------ |
| Emotion Category        | English  | https://github.com/NVIDIA/sentiment-discovery                |
|                         | Chinese  | https://ai.baidu.com/tech/nlp_apply/emotion_detection        |
| Emotion Lexicon         | English  | `resources/English/NRC`                                      |
|                         | Chinese  | `/resources/Chinese/大连理工大学情感词汇本体库`                |
| Emotional Intensity     | English  | `resources/English/NRC`                                      |
|                         | Chinese  | `/resources/Chinese/大连理工大学情感词汇本体库`                |
| Sentiment Score         | English  | [nltk.sentiment.vader.SentimentIntensityAnalyzer](https://www.nltk.org/api/nltk.sentiment.html#nltk.sentiment.vader.SentimentIntensityAnalyzer) |
|                         | Chinese  | `resources/Chinese/BosonNLP`                                 |
| Other Auxilary Features | English  | [Wiki: List of emoticons](https://en.wikipedia.org/wiki/List_of_emoticons), `resources/English/HowNet`, `resources/English/others` |
|                         | Chinese  | `resources/Chinese/HowNet`, `resources/English/others`       |

## Code

### Requirements

```
Python==3.6.10
Keras==2.1.2
Tensorflow==1.13.1
Tensorflow-GPU==1.14.0
```

### Usage

#### Step1: Preprocess

##### Step1.1: Get the `labels`

```
cd code/preprocess
python output_of_labels.py
```

