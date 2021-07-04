# Challenges in Deploying Machine Learning: a Survey of Case Studies

The goal of [the paper](https://arxiv.org/pdf/2011.09926.pdf) is to show that **practitioners face problems** at each stage of the **ML workflow** and to raise awareness with regards to this topic.

*@Safouane*: Some of the problems listed don't happen because of technical difficulties but also because of project scoping and lack of maturity of building and deploying AI solutions in companies.

## Table of content

- [ML deployment workflow](#ml-deployment-workflow)
- [Data management](#data-management)
- [Model learning](#model-learning)
- [Model deployment](#model-deployment)
- [Cross-cutting aspects](#cross-cutting-aspects)
- [Discussion of potential solutions](#discussion-of-potential-solutions)



## ML deployment workflow

The workflow adopted in the paper **Data management => Model learning => Model verification => Model deployment**. 

The problems faced at each step are discussed + cross-cutting problems (ethics, etc).

## Data management

**Data collection** is often a hurdle. Data usually dispersed among many services + data scientist don't have a clear idea what data is available or can be obtained. => Example of twitter services.

**Data preprocessing** becomes difficult when using different sources with different ways of encoding some data, specially if it's the one to merge on. => Example of merging spatial data with different way of encoding it.

**Data augmentation**: Labels assignment can be difficult in some fields for 3 reasons: 

- limited access to experts (e.g: medical field)
- sheer volume (e.g: huge amount of data in networking which makes it difficult to say whether each packet is malicious or not)
- Lack of access to high-variance data (e.g: RL training and real world)

**Data analysis:** Lack of data profiling tools. A survey result: Data issues main reason to doubt quality of the overall work.

## Model learning

**Model selection:** Despite the focus on deep learning in research, industry uses less complex models because they are **easy to deploy** , don't consume that much when it comes to **resources** specially in a hardware constrained environment and usually **interpretable in business domain terms**.

**Training:** Big models (e.g NLP models) training is costly ($50k->$1.6m) + Energy consumption/CO2. 

*@Safouane*: Almost no company retrains these models => use of transfer learning.

**Hyper-parameter selection**: Optimization for hyperparameters is very expensive, specially when it comes to DL models. 

**Model verification**: A model should generalize well, handle edge-cases and satisfy functional requirements. Some challenges with respect to this are:

- **Requirement encoding:** Define business requirements of the model and encode business needs into the model. Getting a good performance on technical metrics doesn't always translate to business metrics improvement.

- **Formal verification:** verify that the model functionality follow the requirements defined + regulations if any. The part pertaining to the requirements that are defined is often not done in industry.

  *@Safouane*: In my experience, it's because the whole context of building a model includes many teams and the separation zone between teams responsibilities is often a grey zone + Data scientist often limit themselves to the technical aspect of the model but this thinking should evolve as the ML ecosystem in companies matures with time.

- **Test-based verification:** testing the model power of generalization is usually done on a subset of the training data or in a simulation environment for RL. Testing the model in a real environment is important.

  *@Safouane*: One can use shadow or canary deployment.

## Model deployment

Issues in industry arise from lack of best practices when it comes to MLOps as well as other reasons. Issues discussed with regards to:

- **Integration:** of a model is composed of tow main activities, building the infra to run the model and implementing the model.

  - Lack of reusing code, data and models internally
  - Include researchers/data scientist (role: build models) and software engineers(build/maintain infra to run models) in the whole process. Their areas of concern overlap as there is no clear separation, so it'd better for them to work hand in hand from the start

- **Monitoring**:

  - Lack of understanding in ML community of the key metrics to monitor
  - Difficulty to adapt out-of-the-box tools to everyone's specific model. ML models need custom monitoring.

- **Updating:**

  - **Necessity to update models** can arise for different reasons: data drift, concept drift, etc

    *@Safouane*: Check evidentlyai blog posts for an answer for when

  - **Model delivery** to a production environment and the infrastructure question: how often can it be done? Could it be automated? ML pipelines contain not only code but also models and data => Need to adapt continuous delivery philosophy to ML

## Cross-cutting aspects

- **Ethics:** impacts the whole pipeline from data collection to the impact of the model which might be misused either intentionally or not.
- **End users' trust:** 
  - Model interpretability has limits as a trust-building tool
  - Invest time in building specialized user interfaces with tailored user experience (geared towards end-users)
  - Using explainable models is preferred when the target audience has experience and an understanding of ML.
  - Explainability is a must-have feature for most of the stakeholders, executives, etc
- **Security**: Practitioners are not equipped to deal with attacks on their ML systems. Focus on 3 adversarial attacks
  - *Data poisoning*: Corrupt integrity of training data. Happens usually when the model is trained continually with live data (e.g. Microsoft twitter bot).
  - *Model stealing*: Reverse engineer the outcomes of a model by sending inputs through an API and getting its outputs (you get the mapping X->y). The goal is usually to build a substitute model.
  - *Model inversion*: Recover training data by exploiting models that report confidence values along their prediction and by having access to a model (through an API for example).

## Discussion of potential solutions

Two ways to go about it, either having **specific tools/choosing a specific platform to target an ML problem** *or* opt for **holistic approaches** like rethinking the whole infrastructure (Moving from microservices to Data Oriented Architectures). This second solution is very time consuming. When it comes to the first solution, as there is a frenzy in the creation of ML solutions, it's hard to choose.

*@Safouane*: Take a look at [this blog](https://engineering.atspotify.com/2019/12/13/the-winding-road-to-better-machine-learning-infrastructure-through-tensorflow-extended-and-kubeflow/) to see how Spotify went about it

