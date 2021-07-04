The goal of the paper is to show that **practitioners face problems** at each stage of the **ML deployment workflow** and to raise awareness with regards to this topic.

@Safouane: Some of the problems listed don't happen because of technical difficulties but also because of project scoping and lack of maturity of building and deploying AI solutions in companies.

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

**Training:** Big models (e.g NLP models) training is costly ($50k->$1.6m) + Energy consumption/CO2. @Safouane: Almost no company retrains these models => use of transfer learning.

**Hyper-parameter selection**: Optimization for hyperparameters is very expensive, specially when it comes to DL models. 

**Model verification**: A model should generalize well, handle edge-cases and satisfy functional requirements. Some challenges with respect to this are:

- **Requirement encoding:** Define business requirements of the model and encode business needs into the model. Getting a good performance on technical metrics doesn't always translate to business metrics improvement.

- **Formal verification:** verify that the model functionality follow the requirements defined + regulations if any. The part pertaining to the requirements that are defined is often not done in industry.

  @Safouane: In my experience, it's because the whole context of building a model includes many teams and the separation zone between teams responsibilities is often a grey zone + Data scientist often limit themselves to the technical aspect of the model but this thinking should evolve as the ML ecosystem in companies matures with time.

- **Test-based verification:** testing the model power of generalization is usually done on a subset of the training data or in a simulation environment for RL. Testing the model in a real environment is important.

  @Safouane: One can use shadow or canary deployment.

## Model deployment

