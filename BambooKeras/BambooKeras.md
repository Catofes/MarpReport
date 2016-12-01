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

* Make sure Python and Pip was installed (We may use Python2 for default). 
* Make sure CUDA was installed.
* `apt-get install python-scipy python-pil`
* `pip install keras`

The **Keras** use **Theano** as default backend. You may need manually install **TensroFlow** if you want.

---
# Install
* Get the GoogLeNet code. [Gitlab](http://pandax.physics.sjtu.edu.cn:8699/qiaohao/BambooKeras) in our server or [Origin Github Gist](https://gist.github.com/joelouismarino/a2ede9ab3928f999575423b9887abd14).
* Run `python googlenet.py` once. Error will happened and ignore it. 
* Modify `~/.keras/keras.json` to
```
{
    "image_dim_ordering": "th",
    "epsilon": 1e-07,
    "floatx": "float32",
    "backend": "theano"
}
```
---
# Install
* Now run `python googlenet.py` again with `cat.jpg` in same folder.
* The predict speed is very slow. May caused by no GPU supported. How to enable GPU support can be find in [here](https://keras.io/getting-started/faq/#how-can-i-run-keras-on-gpu). Use flowing command to force start gpu. Much more slower. No idea why, maybe K80 is different from other nvidia gpu?
```THEANO_FLAGS=device=gpu,floatX=float32 python googlenet.py``` 
* Maybe we can use tensorflow when we train the data.

---
## Test in myself computer.
* Without GPU:
```
Using Theano backend.
NVIDIA: no NVIDIA devices found
285 281 281
7.46user 0.11system 0:07.61elapsed 99%CPU (0avgtext+0avgdata 217356maxresident)k
0inputs+0outputs (0major+98443minor)pagefaults 0swaps
```
* With GPU:
```
Using Theano backend.
285 281 281
7.30user 0.71system 0:08.11elapsed 98%CPU (0avgtext+0avgdata 218400maxresident)k
0inputs+0outputs (0major+100072minor)pagefaults 0swaps
```

---
### Test in myself computer.
* Force use gpu
```
Using Theano backend.
Using gpu device 0: GeForce GTX 860M (CNMeM is disabled, cuDNN not available)
285 281 281
8.62user 0.51system 0:09.22elapsed 99%CPU (0avgtext+0avgdata 282508maxresident)k
0inputs+0outputs (0major+127330minor)pagefaults 0swaps
```

* Maybe predict do not use GPU much? 
* Maybe load data to GPU take too much time?

---
### Test in myself computer.

* Predict Once With GPU
```
Using Theano backend.
Start Compile: 1480571014.7049115
Start Predict: 1480571014.7615883
Finish Predict: 1480571020.1698854
```
* Predict 10 Times With GPU
``` 
Using Theano backend.
Start Compile: 1480571085.462333
Start Predict: 1480571085.5205538
Finish Predict: 1480571099.3852205
285 281 281
```
---
### Test in myself computer.
* Predict Once Without GPU
``` 
NVIDIA: no NVIDIA devices found
Start Compile: 1480571393.2015874
Start Predict: 1480571393.2558823
Finish Predict: 1480571398.9788418
285 281 281
```
* Predict 10 Times Without GPU
```
NVIDIA: no NVIDIA devices found
Start Compile: 1480571318.8493147
Start Predict: 1480571318.905022
Finish Predict: 1480571332.770785
285 281 281
```
---
### Test in myself computer.
* Seems GPU do not accelerate prediction.
* Maybe caused by theano.
* GPU may accelerate in training. 

|281->tabby cat|284->Siamese cat|
|:-:|:-:|
|<img src="./cat.jpg" alt="Drawing" style="height: 250px;"/>|<img src="./cat1.jpg" alt="Drawing" style="height: 250px;"/>|


---
# Average Length Study
* For U238 and Th232, energy range is (2395.2 - 2520.5) keV.
##### U238, Th232 in barrel. Max length in X axis.

<img src="./2016-11-30%2020-34-56%20的屏幕截图.png" alt="Drawing" style="width: 400px;"/>
<img src="./2016-11-30%2020-39-00%20的屏幕截图.png" alt="Drawing" style="width: 400px;"/>

---
# Average Length Study
* Other Axiss are same for U and Th. The length is much longer than we except. I think that was caused by Gamma. I'll check the data.
##### Signal. Max length in X axis. (LogY in left.)
<img src="./2016-11-30%2020-45-43%20的屏幕截图.png" alt="Drawing" style="width: 400px;"/>
<img src="./2016-11-30%2020-47-37%20的屏幕截图.png" alt="Drawing" style="width: 420px;"/>

---
# Average Length Study
* From signal length info we can get that most signal track length in one axis are under 400 mm. 
* GoogLeNet use 224x224 pixels image.(Not so sure)
* Maybe we can use 672x672mm as input hits' range.
