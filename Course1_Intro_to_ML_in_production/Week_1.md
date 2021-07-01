**Lecture** 2: 

The requirements surrounding ML infrastructure

![image-20210701101230650](../_assets/Week_1/image-20210701101230650.png)



**Lecture 3: Steps of an ML Project**

![image-20210701101834491](../_assets/Week_1/image-20210701101834491.png)



**Lecture 4: Case study - speech recognition**

1- In the scoping stage

- Decide to work on speech recognition for voice search
- Decide on key metrics
  - Accuracy, latency, throughput
- Estimate (guestimate) resources and timeline

2 - In the Data stage:

- Is the data labeled consistently?
- How much silence before/after each clip?
- How to perform volume normalization?

3- Modeling

As a starting point, use some open-source code from Github and try in on the data. Performing error analysis will help you target which kind of data to collect more of, how to adapt it to the task and also how to modify the code (model). But focus on the data!

![image-20210701103714869](../_assets/Week_1/image-20210701103714869.png)

When error-analysis suggests that your model is good enough, you can go to Deployment!

4- Deployment

