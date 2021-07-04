The goal of the paper is to show that **practitioners face problems** at each stage of the **deployment process** and to raise awareness with regards to this topic.

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

