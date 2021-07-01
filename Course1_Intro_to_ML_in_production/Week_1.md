# The Machine Learning Project Lifecycle



## Lecture 1: Welcome 

The requirements surrounding ML infrastructure

![image-20210701101230650](../_assets/Week_1/image-20210701101230650.png)



## **Lecture 2: Steps of an ML Project**

![image-20210701101834491](../_assets/Week_1/image-20210701101834491.png)



## Lecture 3: Case study - speech recognition

### 1- In the scoping stage

- Decide to work on speech recognition for voice search
- Decide on key metrics
  - Accuracy, latency, throughput
- Estimate (guestimate) resources and timeline

### 2 - In the Data stage:

- Is the data labeled consistently?
- How much silence before/after each clip?
- How to perform volume normalization?

### 3- Modeling

As a starting point, use some open-source code from Github and try in on the data. Performing error analysis will help you target which kind of data to collect more of, how to adapt it to the task and also how to modify the code (model). But focus on the data!

![image-20210701103714869](../_assets/Week_1/image-20210701103714869.png)

When error-analysis suggests that your model is good enough, you can go to Deployment!

### 4- Deployment

For this example, the deployment infrastructure looked like this

![image-20210701111100518](../_assets/Week_1/image-20210701111100518.png)

***Concept/Data drift*** example: System trained on adult voices, failed when dealing with teens voices. The data distribution changed between the training and the real world.



