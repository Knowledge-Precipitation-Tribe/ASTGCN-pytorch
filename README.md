# ASTGCN-pytorch

This is a pytorch implementation of  Attention Based Spatial-Temporal Graph Convolutional Networks (ASTGCN) model from the paper "[Attention Based Spatial-Temporal Graph Convolutional Networks for Traffic Flow Forecasting]()"

Try to rewrite the [MXNet](https://mxnet.incubator.apache.org/) version [ASTGCN](https://github.com/Davidham3/ASTGCN) using [PyTorch](https://pytorch.org/). Please refer to the MXNet version for more details.

## Attention

The code of this project is runnable, but the result have some program.It will be updated later as improvements are finished.

## Model architecture

![model architecture](https://github.com/Knowledge-Precipitation-Tribe/ASTGCN-pytorch/blob/master/images/model.png)

## Requirements:

- python >= 3.5
- pytorch >= 1.1.0
- Scipy

# Datasets

> Dataset description cites the original article

We validate our model on two highway traffic datasets PeMSD4 and PeMSD8 from California. The datasets are collected by the Caltrans Performance Measurement System ([PeMS](http://pems.dot.ca.gov/)) ([Chen et al., 2001](https://trrjournalonline.trb.org/doi/10.3141/1748-12)) in real time every 30 seconds. The traffic data are aggregated into every 5-minute interval from the raw data. The system has more than 39,000 detectors deployed on the highway in the major metropolitan areas in California. Geographic information about the sensor stations are recorded in the datasets. There are three kinds of traffic measurements considered in our experiments, including total flow, average speed, and average occupancy.

We provide two dataset: PEMS-04, PEMS-08

1. PEMS-04:

   307 detectors
   Jan to Feb in 2018
   3 features: flow, occupy, speed.

2. PEMS-08:

   170 detectors
   July to Augest in 2016
   3 features: flow, occupy, speed.

# Configuration

The configuration file config.conf contains three parts: Data, Training and Predict:

## Data

- adj_filename: path of the adjacency matrix file
- graph_signal_matrix_filename: path of graph signal matrix file
- num_of_vertices: number of vertices
- points_per_hour: points per hour, in our dataset is 12
- num_for_predict: points to predict, in our model is 12

## Training

- model_name: ASTGCN or MSTGCN
- device: set device = cpu, or set gpu-0, which means the first gpu device
- optimizer: sgd, RMSprop, adam, see [this page](https://pytorch.org/docs/stable/optim.html) for more optimizer
- learning_rate: float, like 0.001
- epochs: int, epochs to train
- batch_size: int
- num_of_weeks: int, how many weeks' data will be used
- num_of_days: int, how many days' data will be used
- num_of_hours: int, how many hours' data will be used
- K: int, K-order chebyshev polynomials will be used
- merge: int, 0 or 1, if merge equals 1, merge training set and validation set to train model
- prediction_filename: str, if you specify this parameter, it will save the prediction of current testing set into this file
- params_dir: the folder for saving parameters

## Usage

Train model on PEMS04:

```
    python train.py --config configurations/PEMS04.conf 
```

## Reference

Guo S, Lin Y, Feng N, et al. Attention based spatial-temporal graph convolutional networks for traffic flow forecasting[C]//Proceedings of the AAAI Conference on Artificial Intelligence. 2019, 33: 922-929.