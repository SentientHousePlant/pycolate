# pycolate ☕

![Banner](https://raw.githubusercontent.com/Jackbytes/pycolate/main/images/cover_image.png)

A python implementation of site percolation, generates datasets and illustrations.

## Aims.

This project primarily generates datasets and illustrations from square lattice site percolation. There is an auxillary program which carries out critical probability estimation using coarse graining with possible interactions.

## Installation.

1. Install the latest version of pycolate:
```python
pip install pycolate
```
2.Import pycolate into your python file:
```python
import pycolate
```
## Creating illustrations.

The `pycolate.Percolation` class is used for creating a single instance of percolation. It takes the following arguments:
```python
Perc = Percolation(width, height, occupation probability)
```
We find the clusters by running:
 ```python
 Perc.cluster_find()
 ````
We display the illustration in a window as so:
```python
...
Perc.pretty_clusters() #OR Perc.simple_clusters() or Perc.only_percolating_cluster()
Perc.display()
```
To save the illsutration we run:
```python
...
Perc.save("PATH")
```
So to generate an illustration of a 50x50 grid where each square has a 0.6 chance of being occupied:
```python
import pycolate

perc = pycolate.Percolation(50,50,0.6)
perc.cluster_find()
perc.pretty_clusters()
perc.display() 
perc.save('PATH')
```
The default size for a square is 10 by 10 pixels. To adjust this one can change the `Percolation.site_size` prior to running any methods.

 If we were running a large simulation we may want the sites to only be 1 pixel each, so we would run the following:
```python
import pycolate

perc = pycolate.Percolation(1000,1000,0.6)

perc.site_size = 1
perc.cluster_find()
perc.pretty_clusters()
perc.display() 
perc.save('PATH')
```
To only display the percolating cluster in the illustration one can use `only_percolating_cluster('your_color')` instead of `pretty_clusters()` to create an illustration of the percolating cluster in the color 'your_color' (Must be a valid PIL color).

To display all the clusters in the same colour one can use `simple_clusters()` instead of `pretty_clusters()`. 

By default both of these methods use 'hotpink' as the default color if no color argument is given.

## Running experiments.
One may not be interested in illustrations and just want numeric data. We can compute many different properties by running the `Percolation.cluster_find()` method. Once this has been run there are many properties one can ask for:
### Properties of the Percolation class.
Property | Explanation |
--- | --- |
mean_cluster_size | The mean cluster size, excluding the percolating cluster. |
sizes | A list of all the cluster sizes, excluding the percolating cluster. |
percolated_size | The size of the percolating cluster. |
percolated | A boolean. True if a percolating cluster formed. False if not |
