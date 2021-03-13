---
title: "Deep Learning"
layout: page
date: 2016-01-23 22:10
tag: DL ML
headerImage: true
projects: true
hidden: true # don't count this post in blog pagination
description: "American Express "
category: project
author: deepanshupariyani
externalLink: false
img: /assets/img/1.jpg
---

**Product Based Neural Network for User Response Prediction**


**ABSTRACT**

To identify customers responsive to marketing offers so they can be properly targeted to increase profitaility.
The market segment under consideration was the small business owners in the U.S. using a credit card for business purposes.
In the past one year, a customer resulted in a 10% increase in spend in the 3 months period after he was approached and given any marketing offer/incentive were 
tagged as profitable/responsive customers (tagged as 1) and the rest tagged as 0.
Data used was collected from the data accumulated in the bank database, which was grouped into four broad categories, transaction data, eligibility data(based on risk factors) and profiling data(product utilization and interaction data) and firmographics data.

The objective was to finally predict which customers are responsive and profitable and hence target them accordingly with more marketing offers to save resources and increase profitability, by capturing patterns in the interaction data of customers and  training a neural network  based on how they have behaved/reacted to offers in the past.

**Methodology**
Neural networks have broad applicability to real world business problems and are successful
when applied in banks. Since neural networks are best at identifying patterns or trends in data, they are well suited for prediction or forecasting needs including customer relationship management, risk
management, sales forecasting, data validation, customer research, target marketing, etc. Neural networks use a set of processing elements or nodes analogous to neurons in the brain. These processing elements are interconnected in a network that can then identify patterns in data once it is exposed to the data, that is, the network learns from experience just as people do. This distinguishes neural networks from traditional computing programs that simply follow instructions in a fixed sequential order.

**Model Architecture**
```python


model=Sequential() 
model.add(Conv2D(50,kernel_size=(3,1),strides=1,activation='relu',input_shape=input_shape))
model.add(MaxPooling2D(pool_size=(2,1)))
model.add(Conv2D(50,kernel_size=(3,1),strides=1,activation='relu'))
model.add(MaxPooling2D(pool_size=(2,1)))
model.add(Conv2D(50,kernel_size=(1,116),strides=1,activation='relu'))
model.add(Flatten())
model.add(Dense(1,activation='sigmoid'))
model.compile(loss=keras.metrics.binary_crossentropy,optimizer=keras.optimizers.Adam(),metrics=['accuracy'])
```



|Layer(Type)	 |output,input_shape  |Param #  |
|---------|---------|---------|
|conv2d_1(Conv2D)     |  (None,50,10,116)       |   200      |
|max_pooling2d_1     |  (None,50,5,116)	       |    0     |
|conv2d_2     | (None,50,3,116)        |  7550       |
|max_pooling2d_2     | (None,50,1,116)        |     0    |
|conv2d_3(Conv2D)     | (None,50,1,1)        |    290050     |
|flatten_1(Flatten)     |(None,50)         |     0    |
|dense_1(Dense)     |   (None,1)      |   51      |

