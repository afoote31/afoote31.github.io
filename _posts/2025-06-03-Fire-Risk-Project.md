---
layout: distill
title: Fire Risk Assessment Project
description: A semester project I worked on to learn about computer vision and convolutional neural network architectures
tags: distill formatting
giscus_comments: true
date: 2025-06-03
featured: false
pretty_table: true
mermaid:
  enabled: true
  zoomable: true
code_diff: true
map: true
chart:
  chartjs: true
  echarts: true
  vega_lite: true
tikzjax: true
typograms: true

authors:
  - name: Aaron Foote

bibliography: 2018-12-22-distill.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).

# toc:
# - name: Equations
# if a section has subsections, you can add them as follows:
# subsections:
#   - name: Example Child Subsection 1
#   - name: Example Child Subsection 2
# - name: Citations
# - name: Footnotes
# - name: Code Blocks
# - name: Interactive Plots
# - name: Mermaid
# - name: Diff2Html
# - name: Leaflet
# - name: Chartjs, Echarts and Vega-Lite
# - name: TikZ
# - name: Typograms
# - name: Layouts
# - name: Other Typography?
  
---

This post is a recap of a course project I worked on for a machine learning course. I was interested in learning how to implement some of the classic neural network architectures for image classification and apply them to something related to conservation. Forest fires are a natural disaster that can cause billions of dollars in damages, but they are also unique in that they humans are often the direct cause. Thus, we can potentially take action to help mitigate their destruction. Some low-tech methods for detecting fires include crowdsourced reporting, aerial patrol, and lookout stations. Data-driven approaches have also been considered, using GIS data to extract topological and natural features of terrain<d-cite key="satelliteRisk1"></d-cite><d-cite key="satelliteRisk2"></d-cite><d-cite key="satelliteRisk3"></d-cite>. Others have worked to use satellige images containing fire to develop automated fire detection tools<d-cite key="activeFireSensing1"></d-cite>.

For this project, I develop a tool that uses satellite data<d-cite key="fireRiskData"></d-cite> to identify areas with high risk of the breakout of a wildfire. The risk labels are determined by the Wildfire Hazard Potential index, a tool maintained by the USDA Forest Service. The scores are determined by wildfire simulation modeling. The associated images that make up the features of the model are collected from the National Agriculture Imagery Program, in which aircraft or satellites capture 60-cm ground sample distance images of agricultural and forest land. Each image is annotated with its longitude and latitude, making it easy to identify the risk label of the area captured in the image, as provided by the Wildfire Hazard Potential index.

This approach is useful due to the availability of aerial imaging data for much of the world. Furthermore, it can be used to identify risk in areas that are difficult to access, which would make the deployment of climate sensors difficult. It can also complement sensor-based approaches, serving as a coarse evaluation of fire risk that is bolstered by models utilizing data from sensors deployed on the ground.

To establish a baseline, first a single dense layer is fit, not leveraging any of the typical tools used in image analysis with neural networks. Next, a simple convolutional network is fit, employing two convolutional layers fed into max pooling layer, ultimately ending with a dense layer taking the pooling layer as input and outputting to the seven node output layer. With these baselines established, tools from the famous neural network architectures VGG-16<d-cite key="vgg"></d-cite> and GoogLeNet<d-cite key="googlenet"></d-cite> are added.

The VGG-16 architecture employs blocks of repeated convolutional layers – with padding to ensure that the size of each layer remains the same – that are then fed into a max pooling layer. Each successive block halves each of the dimensions of the layers, until the convolutions are ultimately flattened and fed to two fully connected layers before being used as input to the classifying output layer. The number of kernels used doubles with each block, adding complexity to the network. Additionally, the two fully connected hidden layers have 4096 nodes each, requiring an immense amount of computation to train. Since the task in this paper is far less complex than that for which VGG-16 is designed for, this paper implements a simplified version that uses the same strategy of iterative blocks of convolution and pooling that grow over time, albeit on a greatly diminished scale. 

The GoogLeNet architecture employs so called ”Inception blocks”, by which the network subverts the traditional sequential feed-forward nature of neural networks. In the Inception blocks, a variety of kernels of different sizes can be used for convolution, and their results (with proper padding) concatenated together with the goal of approximat- ing the optimal kernel size. Occasional max pooling layers with stride 2 are used to halve the size of the layers and maintain a reasonable parameter count. Another element included by the team at Google is including loss at points in the middle network into the overall loss. This is done to mitigate vanishing gradients. Since the network fit for this project is much smaller than GoogLeNet, this loss checkpointing technique is not incorporated. The structure for each of the networks is visualized below.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/baseline2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/simpleCNN2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    These are the architectures for the simple networks. On the left is a network with no convolution, and on the right is a simple convolutional neural network.
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/vggMini2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    My implementation of the the VGG architecture, greatly simplified. What we see are the characteristic blocks of convolutions into poolings.
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/googLeNetMini2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    My implementation of the the googLeNet architecture, greatly simplified. I've included inception blocks with convolutions of various size, but did not include the loss checkpointing, as the network is not nearly complex enough for vanishing gradients to be a big concern.
</div>

For the training workflow, 21,541 images are held out to be used as a test set. Of the remaining 70,331 images, 75% are used for training and 25% are used as a validation set. The batch size is 16 images and each model is trained for 25 epochs. Following the ImageNet competition<d-cite key="ImageNet"></d-cite>, accuracy as well as top-2 are used to evaluate the model. In the case of fire risk evaluation, even if a model does not have the highest accuracy, if it categorizes a given image as an adjacent category or ranks the true category second with high accuracy, that model may in fact be more useful than one with slightly higher accuracy but lower top-2 accuracy.

With just over fifty thousand images to train on, the complexity of the model must be reduced greatly as compared to the complexity of traditional neural network architectures for image classification to prevent overfitting and keep the training time reasonable. Steps taken to regularize are reducing the learning rate of the Adam optimizer to 1 × 10−5 (1 × 10−3 is default), implementing batch normalization on the final dense layer of each network, and incorporating dropout learning in that layer as well, with a dropout rate of 0.4.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/lossPlot.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/accuracyPlot.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/top2AccuracyPlot.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Loss, accuracy, and top-2 accuracy for the models. The baseline model is shown in <span style="color:blue">*blue*</span> 🟦, the simple convolutional model in <span style="color:pink">*pink*</span> 🟣, VGG mini in <span style="color:red">*red*</span> 🔺, and googLeNet mini in black ◾. The training performance is plotted in solid line style and the validation performance in dashed line style.
</div>

As a baseline, the convolution-free neural network performs considerably worse than the rest of the models. However, it interestingly does not overfit as the rest of the models do, as shown by the non-divergence of the training and validation curves for loss, accuracy, and top-two accuracy. The lack of flexibility of just one dense layer seems to prevent the model from capturing the complexities of image data, limiting both the predictive capabilities of the model and the extent to which it can overfit to the data. This confirms the basic intuition that convolutions are a valuable tool for the task of image classification.

The rest of the models all have difficulty with one key issue: overfitting. Despite considerable steps taken to reduce the prevalence of overfitting, the flexibility inherent in the iterative convolutions proves too complex for the limited data available. The more complex that the model gets – simple CNN, then the VGG architecture, with the GoogLeNet architecture as most complex – the greater the divergence between training and validation performance, meaning the greater the overfit.

Despite the varying extents of overfitting, all models with convolutional layers perform similarly in terms of validation loss, validation accuracy, and validation top-two accuracy. To highlight the importance of considering multiple performance metrics, note that even though the baseline model is undeniably worse than the others when compared on accuracy, it is competitive when compared on top-two accuracy. This suggests that even though the simple model is unable to detect the fine nuances that separate between categories, it is surprisingly good at providing a ballpark estimate of the risk.

Examining the performance of each of the models on a held out test set of 21,541 images, it can be seen that despite the overfitting, the complex models do in fact generalize best to the test set. The baseline model is far and away worst performing, with the simple convolutional network serving as a middle ground. The enhanced architectures perform similarly in accuracy and top two accuracy, but the GoogLeNet architecture has by far the lowest loss, making it the best performing model fit in this project.


|   Model         | Loss | Accuracy  | Top-2 Accuracy |
|   :---------:   | :--: | :-------: | :------:       |
| Baseline        |1.563 |   0.409   | 0.655          |
| Simple CNN      |1.456 |   0.463   | 0.669          |
| VGG Mini        |1.422 |   0.507   | 0.694          |
| GoogLeNet Mini  |1.338 |   0.503   | 0.707          |



