# Hidden Technical Debt in Machine Learning Systems

[This article](https://papers.nips.cc/paper/2015/file/86df7dcfd896fcaf2674f757a2463eba-Paper.pdf) discusses technical debt linked to ML systems and proposes ways of mitigating some of the problems listed.

ML systems in this article are represented as follows:

![image-20210706014549818](../../_assets/C1W1_references_summary/image-20210706014549818.png)





## Table of content

- [Complex models erode boundaries](#complex-models-erode-boundaries)
- [Data Dependencies Cost More than Code Dependencies](#data-dependencies-cost-more-than-code-dependencies)
- [Feedback loops](#feedback-loops)
- [ML-system anti-patterns](#ml-system-anti-patterns)
- [Configuration debt](#configuration-debt)
- [Dealing with changes in the external world](#dealing-with-changes-in-the-external-world)
- [Other areas of ML-related debt](#other-areas-of-ml-related-debt)



## Complex models erode boundaries

Software engineering practices like abstraction and modular design that creates maintainable code (+ isolated changes) don't apply to ML systems.

**Entanglement:** Changing anything changes everything. The slightest change (adding a feature, removing one, change in hyperparameters) can't be isolated. Solution: Use ensembles if errors are uncorrelated with the existing model mA.

**Correction cascades:** Solving a problem *A'* by building a model *mA*' on top of a model *mA* that solves a similar problem *A*... This cascading of models creates an improvement deadlock, no model lower in the chain can be improved without system-level detriments. Solution: either augment mA to solve A' or build a separate model mA'.

**Undeclared consumers:** When dealing with pressing deadlines, people will use any usable signal at hand. Undeclared consumers create undeclared cascades + they can create hidden feedback loop. Solution: Guard against this behavior with (e.g) access restrictions.

## Data Dependencies Cost More than Code Dependencies

**Unstable data dependencies:** Improvements or ramifications to an input signal (or an unstable input signal over time) have arbitrary impact on the consuming ML system and are costly to diagnose and address. Solution: When diagnosing, a system of data versioning may help but this comes with some overhead of its own.

**Underutilized data dependencies**: These are input signals that provide little incremental modeling benefit. Solution: These can be detected via exhaustive leave-one-feature-out evaluations.

**Static analysis of data dependencies**: Tools for error checking, tracking down consumers and forcing migration and updates are not that common.

## Feedback loops

ML systems in some cases end up influencing their own behavior and this creates an analysis debt as it becomes difficult to predict the behavior of a certain model. This happens under tow main forms.

- **Direct feedback loops**: A model influences the selection of its own future training (when online training or retraining on live data). This happens for example when the model impacts the behavior of customer (e.g: recommendation systems). Solution: Using randomization or isolating parts of data from being influenced by a given model.
- **Hidden feedback loops**: Two systems impact each other, a change in one system leads to a change in a second one even if the two are somehow independent. Two stock market prediction models by two different companies, in case there is an improvement to one of them or a bug, it influences the bidding behavior of the other. 

## ML-system anti-patterns

**Glue code**: Much of the code surrounding the usage of open-source ML packages is there just to glue the rest of the system to the open-source package that is used. This glue-code is very solution dependent. This pattern should be avoided. Solution: Create a clean native solution or wrap the package into a common API.

**Pipeline jungles**: A special case of glue code, the code for preparing data often becomes a jungle of joins, sampling steps, intermediate outputs. Managing these pipelines is costly. Solution: Have engineers and researchers work on the project hand in hand.

**Dead experimental codepaths**: Avoid having many codepaths in your code, opt for low cyclomatic complexity and remove any unused codepaths. This should help avoiding errors and eases the task of backward compatibility.

**Abstraction debt**: Lack of abstractions/right interfaces in the ML community; what is the right interface to describe a stream of data a model, a prediction?

**Common smells**:

- ***Multiple-Language smell***: tempting but costly (difficulty of maintenance + transferring ownership)
- ***Prototype smell***: Prototyping environment has its own costs and if it tends to be used as production environment, that is an indicator that the production environment is brittle + results found at small scale don't always reflect the reality at full scale. Don't use the two environments interchangeably.

## Configuration debt

A messy configuration is hard to maintain and error-prone. A good configuration should be easy to read (visually) and modify, hard to make manual errors, possible to detect redundant settings and should undergo a full code-review and be check into a repo.

## Dealing with changes in the external world

As the external world is not stable, models need to be updated/changed.

**Fixed thresholds in dynamic systems:** thresholds that are selected during the training phase are often manually set. If need to change => brittle and time-consuming. Better learn the thresholds (as an additional hyper-parameter)

**Monitoring and testing**: Difficult to know what to monitor but some metrics should remain invariants over time

- **Prediction bias**: the distribution of predicted labels should be the same as the one of observed labels in training. If the distribution changes, it might be indicative of a change in the world behavior.
- **Action limits**: if a system does some action (e.g: make biddings), it's good to enforce action alert if some action is triggered way too much.
- **Up-stream producers**: if any problem with upstream data, propagate the alert to the downstream ML system and to the users of the outputs of the ML system.

Automatic intervention as a result of alerts should be favored to human intervention even if it might take time to set up at first.

## Other areas of ML-related debt

**Data testing debt**: Data should be tested (at least some sanity checks)

**Reproducibility debt**: ML experiments are not that reproducible (most algorithms have some kind of randomization)

**Process Management debt**: Maintaining a mature system with many interlinked models is hard in case of data blockage or error in one of them.

**Cultural debt**: ML engineering (e.g. reduction of complexity, improvements in stability) should be encouraged as much as ML research (e.g. high performance)
