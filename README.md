# GNR638_Report1
## Making the invisible visible: Action Recognition through walls and occlusions

### Abstract:
Understanding people's actions and interactions typically depends on seeing them. Automating the process of action recognition from visual data has been the topic of much research in the computer vision community. But what if it's too dark or the person is occluded or behind a wall? In this paper, a Neural Network Model is introduced that can detect human actions through walls and occlusions, and in poor lighting conditions. 

The model takes radio frequency(RF) signals as input, generates 3D human skeletons as an intermediate representation, and recognizes actions and interactions of multiple people over a time. By translating the input to intermediate skeleton model, our model can learn from both vision based and RF based datasets, and allow the two tasks to help each other. A comparable accuracy is achieved even in the case when people are not visible.

### Introduction

Action recognition is defined as detecting and classifying human actions from a time series(video frames,human skeleton sequences, etc). When the camera is fixed or a person is occluded for greater amount of time(ex- person going into another room), action recognition approach fails. Basically, cameras also suffer from same limitation as our eyes i.e. our eyes sense only visible light.
Radio frequencies reflect off human body and traverse through walls or occlusions to detect action.

Previous models poorly generalize to new environments or people and is senitive to lighting conditions.Also, they cannot deal with multi-purpose actions. This paper acts as a bridge between these drawbacks.

Feasibility of keeping human skeletons as intermediate representation is advantageous because:
1] It enables the model to train with both RF and vision data, and leverage existing vision-based 3D skeleton datasets such as PKU-MMD and NTU-RGB+D 
2] it allows additional supervision on the intermediate skeletons that helps guide the learning process beyond the mere action labels used in past RF-based action
recognition systems
3] it improves the model’s ability to generalize to new environments and people because the skeleton representation is minimally impacted by the environment or the subjects’ identities.

The model is augmented with two innovations that improve its performance -
- For skeletons, particularly generated from RF signals, can have errors and mispredictions. To deal with this problem, our  intermediate representation along with the skeleton includes a time-varying confidencescore at each point. Self attention is used allow the model to attend to different joints over time differently, depending on their confidence scores.
- The model can tackle situations where multiple people interact or are engaged in different actions simultaneously

**Dataset:** Action Detection dataset from diiferent environments with a wireless device and multi camera system. The dataset spans 25 hours and contain 30 individuals performing various single person and multi-person actions.

**Mean Average Precision**
- RF dataset 87.8%(without occlusion)
- RF dataset 83.0%(with occlusion)

_Multimodal training_(Multimodal learning suggests that when a number of our senses - visual, auditory, kinaesthetic - are being engaged during learning, we understand and remember more. By combining these modes, learners experience learning in a variety of ways to create a diverse learning style) improves detection for both the visual as well as wireless modalities.

The paper has the following contributions:
• It presents the first model for skeleton-based action recognition using radio signals; It further demonstrates that such model can accurately recognize actions and interactions through walls and in extremely poor lighting conditions using solely RF signals
• The paper proposes “skeletons” as an intermediate representation for transferring knowledge related to action recognition across modalities, and empirically demonstrate that such knowledge transfer improves performance.
• The paper introduces a new spatio-temporal attention module, which improves skeleton-based action recognition regardless of whether the skeletons are generated
from RF or vision-based data.
• It also presents a novel multi-proposal module that extends skeleton-based action recognition to detect simultaneous actions and interactions of multiple people.

### Related Works
1] Video Based Action Recognition:Image descriptors like HOG and SIFT have been extended to 3D [6, 27] to extract temporal clues from videos are specially designed to track motion information in videos.More recent solutions are based on deep learning, and fall into two main categories. The first category extracts motion and appearance features jointly by leveraging 3D convolution networks. The second category considers spatial features and temporal features separately by using two-stream neural networks .

2] Skeleton Based Action Recognition: Its advantages are first, skeletons provide a robust representation for human dynamics against background noise. Second, skeletons are more succinct in comparison to RGB videos, which reduces computational overhead and allows for smaller models suitable for mobile platforms.
Prior work on skeleton-based action recognition can be divided to three categories. Early work used Recurrent Neural Networks (RNNs) to model temporal dependencies in skeleton data . Recently, however, the literature shifted to Convolutional Neural Networks (CNNs) to learn spatio-temporal features and achieved impressive performance. Also, some papers represented skeletons as graphs and utilized graph neural network (GNN) for action recognition.

In our work, we adopt a CNN-based approach, and expand on the Hierarchical Co-occurrence Network (HCN) model by introducing a spatio-temporal attention module to deal with skeletons generated from wireless signals, and a multi-proposal module to enable multiple action predictions at the same time.

3] Radio Based Action Recognition: 
This is carried out by two methods. The first is similar to RF action in that analyses the radio signals that bounce of people's bodies. They use action labels for supervision, and simple classifiers. They recognize only simple actions such as walking, sitting,running, and a max upto 10 actions. Also, they deal with only single person scenarios. The second one is that they deploy a network of sensors for different actions and recognize the subject actions based on which body parts move.

Spatial(w.r.t space) and temporal(w.r.t time)

### Method


