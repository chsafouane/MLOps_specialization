# Monitoring ML models in production

Notes taken while reading https://christophergs.com/machine%20learning/2020/03/14/how-to-monitor-machine-learning-models/

------

## Why it's hard?

ML systems have all the **challenges of traditional code + ML-specific challenges** as an ML system is not just code, it also includes a model and data fed to it. A change in any one component impact the other (e.g: A change in a data feature impact the output of the model)

ML systems span different teams (Data scientists, DevOps, Business, etc), each team uses its own lingo => It's important to **define terms** to avoid confusion.

## Why monitor?

- **Data skews**: Training data differs from live data (artificial data used in training, different data sources/databases used, etc)
- **Model staleness**: The environment changes and so should the model (consumer behavior change, shifts in habits, adversarial scenarios)
- **Negative feedback loops**: if a model is trained on data collected in production and this data is corrupted, then the model will perform poorly (this happens often in recommendation systems or any system that impacts the consumer behavior)

Monitoring is all about managing risks that come at **post-production stage**. ML systems can go wrong in two main ways:

- **Data science issues**: data monitoring, prediction monitoring
- **Operations issues**: system monitoring

## Data science monitoring

Usually, it's not possible to know the accuracy of a model immediately. One has to wait for days/weeks to get its accuracy => **Monitor proxy values to model accuracy in production**

- **Model input monitoring**: values within an allowed set or within a specific range + monitoring null values if allowed as entries
- **Model prediction monitoring**: Statistical tests for basic statistics (mean, median, std, max/min values, etc)
- **Model versions**: it should be easy to track which version of the model is deployed

## Operations monitoring

This kind of monitoring is well established in software engineering. Operational concerns around ML systems consist of system performance (Latency/IO/Memory/Disk utilization), system reliability (Uptime) and auditability.

@Safouane: I think auditability will be a key element with all regulatory frameworks being implemented nowadays (RGPD).

## Metrics and Logs

Metrics are a good fit for operational concerns of an ML system as well as for prediction monitoring. Prometheus and Grafana are good candidate to create dashboards that track standard statistical metrics and automate alerts.

When it comes to inputs, using logs seems a better fit as inputs might have high cardinality and having metrics for inputs with high cardinality doesn't seem like a good idea. Using Kibana (and the elastic stack with it) to setup dashboard to track the ML model input values and automate alerts  is a good fit for this task.

