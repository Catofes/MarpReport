<!-- $theme: gaia -->

<!-- page_number: true -->
# BambooKeras
#### Hao Qiao 
###### Peking University
---

# Introduction

* Keras is a high-level neural networks library, written in Python and capable of running on top of either TensorFlow or Theano. 
* TensorFlow and Theano can use GPU(CUDA) to accelarate the compute.
* We may use GoogLeNet to classify the signal and background.      

---

# Install

* Make sure Python and Pip was installed. 
* Make sure CUDA was installed.
* `apt-get install scipy==0.18.1`
* `pip install keras`

The **Keras** use **Theano** as default backend. You may need manually install **TensroFlow** if you want.

---
# Install
* Get the GoogLeNet code. [Gitlab](http://pandax.physics.sjtu.edu.cn:8699/qiaohao/BambooKeras) in our server or [Origin Github Gist](https://gist.github.com/joelouismarino/a2ede9ab3928f999575423b9887abd14).

---
# Average Length Study
* For U238 and Th232, energy range is (2395.2 - 2520.5) keV.
##### U238, Th232 in barrel. Max length in X axis.

<img src="/home/herbertqiao/Pictures/2016-11-30%2020-34-56%20的屏幕截图.png" alt="Drawing" style="width: 400px;"/>
<img src="/home/herbertqiao/Pictures/2016-11-30%2020-39-00%20的屏幕截图.png" alt="Drawing" style="width: 400px;"/>

---
# Average Length Study
* Other Axiss are same for U and Th. The length is much longer than we except. I think that was caused by Gamma. I'll check the data.
##### Signal. Max length in X axis. (LogY in left.)
<img src="/home/herbertqiao/Pictures/2016-11-30%2020-45-43%20的屏幕截图.png" alt="Drawing" style="width: 400px;"/>
<img src="/home/herbertqiao/Pictures/2016-11-30%2020-47-37%20的屏幕截图.png" alt="Drawing" style="width: 420px;"/>

---
# Average Length Study
* From signal length info we can get that most signal track length in one axis are under 400 mm. 
* GoogLeNet use 224x224 pixels image.(Not so sure)
* Maybe we can use 672x672mm as input hits' range.
