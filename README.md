# PathBee: Accelerating Shortest Path Querying via Graph Neural Networks

This repository hosts the source code and supplementary materials for our VLDB 2024 submission, "PathBee: Accelerating Shortest Path Querying via Graph Neural Networks". This work presents PathBee, an innovative framework leveraging Graph Neural Networks (GNNs) that significantly advances the current 2-hop labeling-based approaches.

## PathBee Workflow

Our workflow is comprised of four key stages:

1. **Training Data Preparation**: We generate synthetic scale-free graphs using the NetworkX library, and then annotate the data using an internal tool that calculates precise centrality values.
2. **GNN Model Training**: We use the prepared datasets to train our GNN model.
3. **GNN Model Inference**: This stage is dedicated to predicting Betweenness Centrality (BC) values.
4. **Execute 2-Hop Labeling**: We utilize the predicted BC values to sort vertices and execute the 2-Hop Labeling algorithm.

<div align=center><img alt="WORKFLOW"src="assets\pipeline.png"/></div>


## Quick Start

### Step 1: Training Data Preparation

```sh
# Generate dataset
python launch.py gen
```

### Step 2: GNN Model Training

```sh
# Train the GNN model 
python launch.py train
```

### Step 3: GNN Model Inference

```sh
# Run GNN model inference to predict BC values
python launch.py infer

```

### Step 4: Execute 2-Hop Labeling

```sh
# Compile the 2-Hop Labeling algorithm
python launch.py indexing

```

## Performance

### Baseline

PathBee is a general framework that can be used with various 2-hop labeling algorithms. The central component shared among these algorithms is the pruned index construction procedure. This repository demonstrates the effectiveness and versatility of PathBee by applying it to the representative offline 2-hop labeling algorithm, PLL [1], within the pruned index construction procedure. For in-depth insights into PathBee's integration with different algorithms, please refer to our paper for detailed information.

### Setup

For experiments in a single-core CPU environment, we use a Linux server with AMD Ryzen 7 3700X (3.6 GHz) and 128 GB of main memory. For experiments in a multi-core CPU environment, we use a Linux server with Intel(R) Xeon(R) CPU E5-2696 v4 (2.2 GHz, 80 cores) and 128 GB of main memory. The cut-off time is set to 12 hours.

### Effectiveness of PathBee on PLL

We conducted a comparison of the index construction time, index size and query time between PLL, PathBee, and PathBee+ on 26 real-world datasets.

The performance comparison result is shown as below.

#### Comparison on Index Construction Time

<div align=center><img alt="pll_IBT"src="assets\pll_IBT.png"/></div>

#### Comparison on Index Size

<div align=center><img alt="pll_IS"src="assets\pll_IS.png"/></div>

#### Comparison on Query Time

<div align=center><img alt="pll_IT"src="assets\pll_QT.png"/></div>

### Scalability of PathBee
In the experiment for scalability validation, we randomly divide vertices of a graph into 5 equally sized vertex groups and create 5 graphs for the cases of 20%, 40%, 60%, 80%, 100%: the 𝑖-th graph is the induced subgraph on the first 𝑖-th vertex group.

The scalability validation result is shown as below.

#### Scalability Tests

<div align=center><img alt="sca_IBT"src="assets\sca-PAT.png"/></div>

<div align=center><img alt="sca_IS"src="assets\sca-IMDB.png"/></div>

### Traversal Cost Model Validation

The extra traversal cost model validation result (section 4 in our paper) is shown as below.

<div align="center">
  <img alt="sca_IBT" src="assets\model-EPI.png" width="340"/>
  <img alt="sca_IBT" src="assets\model-MOC.png" width="340"/>
</div>

<div align="center">
  <img alt="sca_IBT" src="assets\model-GN.png" width="340"/>
  <img alt="sca_IBT" src="assets\model-SLA.png" width="347"/>
</div>

## References

[1] [Pruned Landmark Labeling](https://github.com/iwiwi/pruned-landmark-labeling)

[2] [GNN-Bet](https://github.com/sunilkmaurya/GNN-Bet)