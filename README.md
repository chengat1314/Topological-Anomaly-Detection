# Topological Anomaly Detection (TAD)

![iris](https://raw.githubusercontent.com/dmarx/topological_anomaly_detection/master/Iris_outlier_graph_small.png)

This script is an implementation of an outlier detection technique described in the paper [Topological Anomaly Detection Performance with
Multispectral Polarimetric Imagery](http://www.cis.rit.edu/~mxgpci/pubs/gartley-7334-1.pdf) by [Dr. Michael Gartley](http://www.cis.rit.edu/~mxgpci/) (2009). 

Algorithm
----------

In essence, the technique is essentially a density based outlier detection algorithm that, instead of calculating local densities, constructs a graph
of the data using nearest-neighbors. The algorithm is different from traditional kNN outlier detection algorithms in that instead of setting 'k' as a
parameter, you instead set a maximal inter-observation distance (called the graph "resolution" by Gartley). If the distance between two points is less 
than the graph resolution, add an edge between those two observations to the graph. Once the full graph is constructed, determine which connected 
components comprise the "background" of the data by setting some threshold percentage of observations 'p': any components with fewer than 'p' observations 
is considered an anomalous component, and all the observations (nodes) in this component are outliers. 

Requires
--------
* networkx
* numpy
* pandas
* scipy

The pandas requirement is just a convenience to return the outlier scores as a pandas.Series. To break this requirement, modify the return value of `calculate_anomaly_scores` 
to just return the `scores` variable (a dict) instead of wrapping it in a pandas.Series.

Usage
---------
Demo usage can be found in the file ```demo.py```. The above image demonstrates the result when TAD is applied to the Iris dataset (observation positions given by PCA). 
NB: The demo requires ```sklearn``` for the iris data and for PCA.