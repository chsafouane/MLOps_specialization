# Evidently AI blog: Machine learning monitoring

These are my own notes that I took when reading the  [Evidently AI Blog](https://evidentlyai.com/blog)

## Why?

Neglecting life after deployment of models is a result of a lack of maturity in companies AI usage.

A model is never final and without performance monitoring, one can't know if the model is performant in production and when its performance starts decaying.

![Machine learning model lifecycle: after model deployment comes model serving and performance monitoring.](../_assets/C1W1_references_summary/model_lifecycle_2.png)

Monitoring models shouldn't boil down to software engineering metrics (the health of a service from a software engineering perspective). It should include software engineering metrics, input and output data metrics, comparison to ground truth and business KPI.

If one waits for business KPI to show the failure, this is already way too late as it the failure has already impacted the company bottom line.

When the model starts failing whether in general or on a specific category, this should be detected quickly. Aggregate metrics can hide model failure on a specific subset of data.

## Who should care?

The **data team** should care as it wants the model to make the right call + problem detection as early as possible. **Business and domain experts** acts on model predictions and wants to know the model weak spots if any show up in production.

**Different metrics** should be monitored, data scientist don't use the same metrics as domain experts + failure detection might be, depending on the problem, easier from a specific perspective => Both business experts and the data team should have access to monitoring tools.

## What are we missing?

Most data science teams monitor models only in the first months and as new project come up, they often let go this task.

The problem in machine learning is that deploying a model often includes different teams: data engineering, data scientist/ML engineers, DevOps as well as an IT team that might be watching over service health. When a model fails, there is no clear separation between territories and this makes it a **grey zone**.

## What can go wrong with data?

- Data can be lost at source: Users actions on a mobile app not logged
- Data processing issues because of lost access, infra update, broken feature code, etc
- Data schema change
- Broken upstream models: a model's input is some model's output. If something's wrong with the 1st, garbage in when it comes to the 2nd.

Monitoring data quality at every step of the pipeline is a basic health check.

## What else can go wrong?

### Drift definition

(In this paragraph, we suppose that data quality is fine)

Models get worse over time with a different speed. This happens for a couple of reasons:

- **Data drift**: the inputs X has changed. This is also called feature drift, population or covariate shift. The model is fine and it does well on data similar to old data, but as new data has changed with regards to the old one, the model does badly now.

  To address data drift, one needs to train the model on the new data or rebuild it for the new segment.

- **Training-serving skew**: It is a mismatch between the training data and the real data. It usually shows up at the first attempt of applying the model to real data. This usually happens when training data is an artificial one.

  When this happens, either collect data or profit from real data coming in while the model in production and use it to retrain the model.

- **Concept drift**: happens when the very meaning of what we are trying to predict evolves, the mapping X->y changes. Sometimes concept drift impact only the relation of one feature Xi to y and not all other features.

  Concept drift ***usually happens gradually*** because the world evolves in a gradual way but this depends on the fields and on events happening in the world.  It is **possible to get an estimate of time needed for a model to age** by imitating the phenomena on old data to which we have ground truth.

  ***Sudden concept drift*** also happen. Mobility models or online purchases models failed because of covid. When a production line is revamped or machines changed, fault prediction models might fail.

### Dealing with drift

- Retrain a new model with more weights on recent data or drop past data if enough is collected.
- Naïve retraining is not always the solution. Sometimes redefining the model scope (e.g. predictions horizon) or the business process is necessary.